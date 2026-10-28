# Arquitetura proposta e critérios de qualidade
Status: planejamento, sem código, dependências instaladas, banco, deploy ou contas criadas.

## Primeira versão: local offline
Recomendação a validar na implementação: TypeScript, Vite, React para interface acessível e Phaser para cenas e animação de sprites.
Renderizador usa apenas imagens aprovadas; não gera cenário ou personagens por primitivas. Versões serão verificadas, fixadas e registradas em lockfile ao iniciar código.
Camadas:
- Domínio independente de UI: turnos, caminhos, economia, inventário e cristais.
- Dados: mapa fixo versionado, eventos, preços, manifesto de assets.
- Aplicação: comandos, validação e eventos resultantes.
- Apresentação: câmera, HUD, sprites, som e animação.
- Adaptadores: persistência local na primeira versão e serviço online depois.
- Bots: enviam comandos legais através da mesma interface que humanos.
Não atrelar resultado da regra ao fim de uma animação ou ao FPS. Animação reproduz eventos já decididos.
Primeiro uso requer instalar dependências/build; depois jogo local não deve depender de CDN, login ou API externa. Entregar instruções Windows e iniciar.bat na fase de código. Service worker para instalação offline é opcional e separado.

## Estado e comandos: contrato conceitual
Estado inclui: versão das regras, versão do mapa, identificador da partida, ordem e assentos, jogador ativo, fase, rodada, revisão, semente/posição do gerador offline, saldo, PT, casas, itens, negócios, status, cinco cristais com dono ou posição, baralhos, efeitos pendentes e vencedor.
Comandos: preparar, trabalhar, usar item, sabotar, rolar dado, escolher caminho, comprar, resolver escolha e encerrar.
Cada comando valida fase, jogador, custo, alvo e revisão. Produz estado seguinte e lista de eventos; operação inválida não consome recursos.
Fases: configuração → preparação → dado → movimento/escolha de rota → resolução → fim de turno → fim de rodada; vitória encerra qualquer fase aplicável.
Sorteio offline reproduzível por semente para depuração. Online: sorteio feito por serviço autoritativo; não publicar estado interno que permita prever próximos resultados.
Salvar apenas estado lógico, nunca tempo parcial de animação. Recarregar retoma ponto seguro de decisão. Exportar/importar save versionado e validar arquivo antes de usar.
IndexedDB para saves, preferências locais separadas; botão de exportação de backup. Migrações explícitas ou mensagem de incompatibilidade, sem corrupção silenciosa.

## Online posterior: GitHub + Vercel + Supabase
- GitHub guarda código, documentação e assets selecionados. Usar Git LFS se volume de masters justificar; validar compatibilidade com build antes.
- Vercel entrega frontend e, se adotado, endpoints curtos de comandos.
- Supabase: Auth, persistência Postgres e Realtime para atualização/presença.
- Proposta de entidades: profiles, rooms, room_members, matches, match_players, match_commands, match_events e snapshots; inventário/cristais no estado canônico com restrições de integridade.
- A autoridade é o serviço: cliente solicita ação, nunca informa saldo final, dado escolhido ou dono final do cristal.
- Cada comando inclui command_id único e expected_revision. Transação bloqueia/revisa estado, valida membro e vez, sorteia, grava estado/eventos e confirma; duplicata devolve resposta original, sem cobrar duas vezes.
- Realtime notifica atualização; snapshot e sequência persistida recuperam mensagens perdidas. Presence não decide abandono nem vitória.
- Canais privados por sala; acesso só de participantes autorizados. Códigos de convite não substituem autorização.
- RLS em todas as tabelas expostas, política por associação à sala; operações de jogo apenas por caminho autoritativo. Segredos ficam fora do navegador.
- Reconexão busca snapshot e eventos posteriores. Queda do criador não deve apagar partida.
- Prazo de ação usa horário persistido do servidor. Inicialmente, vencimento resolvido de forma idempotente na próxima requisição/poll; mecanismo de despertar automático deve ser decidido e testado antes do online público.
- Bot online executado pela autoridade; clientes não podem assumir vaga alheia enviando comandos.
- Métricas e erros sem registrar tokens ou informações sensíveis.
Não abrir infraestrutura nesta etapa. Revalidar documentação, changelog do Supabase e limites/custos Vercel ao integrar. Não prometer suporte a uma partida inteira mantida em memória de função.
Tabelas, políticas, funções e migrações só serão escritas após arte e autorização para implementação.

## Matriz de validação
| Área | Verificação necessária antes do aceite |
|---|---|
| Dado e rotas | 1–6, ajustes legais, bifurcação com passos restantes, sem caminhos presos |
| Cristais | Exatamente cinco identidades conservadas, sem duplicação, coleta em passagem, vitória imediata |
| Sabotagem | Sem alvo inválido, custo correto, escudo, proteção, destinos elegíveis e fallback |
| Economia | Sem saldo negativo, aluguel limitado, renda uma vez por rodada, limites de propriedade |
| Eventos | Encadeamento finito, descarte/embaralhamento, item com inventário cheio |
| Save | Reabrir em cada fase segura, arquivo inválido, versões, nenhuma recompensa duplicada |
| Bots | Comandos legais, sem acesso a sorte futura, partida completa com 1 humano e 7 bots |
| Online | Comandos simultâneos, duplicatas, revisões antigas, queda, reconexão, troca por bot |
| Segurança | Usuário fora da sala não lê/joga, participante não altera saldo/dado, convite revogável |
| Interface | 2/4/8 participantes, mouse/toque/teclado, 360 px, cristais visíveis, movimento reduzido |
| Arte/áudio | Alpha, pivôs, contraste, loops, mute, ausência de dependência de asset externo |
Metas: interface responsiva; 60 FPS em desktop e ao menos 30 FPS estáveis em celular de referência a definir. Não são resultados medidos.
Orçamento inicial: carregamento crítico até 12 MB; demais bairros/FX por carregamento sob demanda. Medir bytes e memória de texturas, não apenas quantidade de arquivos.
Simulações futuras: pelo menos 1.000 partidas por combinação de 2, 4 e 8 assentos para procurar travamentos e medir percentis de duração; complementadas por testes humanos, não substituídas por bots.
Critério de avanço: corrigir falhas de integridade/segurança antes de cosméticos. Sem estimativa de data de lançamento antes do protótipo medido.

## Riscos e resposta
- Cinco cristais globais podem prolongar disputa: monitorar concentração e sabotagem, ajustar preço/proteção com aprovação sem mudar vitória silenciosamente.
- Oito turnos podem causar espera: escolhas rápidas, preparação visual durante vez alheia, animação acelerável.
- Renda pode favorecer líder: propriedade limitada e preço calibrado; sem crescimento exponencial de níveis.
- Arte gerada pode variar entre frames: referência mestre, produção por lotes e revisão quadro a quadro.
- Muitos sprites podem pesar: atlas pequenos, carregamento por grupo e exportações otimizadas.
- Cliente offline é alterável: aceitável para treino local, sem transportar save offline para ranking online.
- Matchmaking amplia abuso: lançar salas privadas primeiro; público só depois de limites, denúncias/bloqueio e reconexão testados.
