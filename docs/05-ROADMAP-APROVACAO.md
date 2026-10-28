# Roadmap e decisões para aprovação — v0.1
Etapas 0 e 1 concluídas; etapa 2 detalhada e conferida estruturalmente; etapa 3 em produção. Não são promessas de prazo.

## Sequência passo a passo
| Etapa | Entrega | Condição de avanço |
|---|---|---|
| 0 — briefing e pesquisa | Requisitos, referências, GDD, arte/HUD, áudio e arquitetura | Documentação inicial entregue neste repositório |
| 1 — aprovação das regras | Decisão registrada sobre os pontos abaixo; GDD v0.2 | Proprietário aprova ou solicita alterações |
| 2 — fechar mapa e produção | Tipos atribuídos aos 60 IDs, posições/arestas e zonas de cristal; catálogo final de imagens | Conferir rotas, custos, coleta e leitura; sem código |
| 3 — conceitos gerados | Concept do tabuleiro, mockup HUD e personagem mestre com carrinho | Aprovação de câmera, estética e significado de “carregando” |
| 4 — sprites estáticos | Oito cores, cinco cristais, casas, cenário, dado, itens e HUD | Assets da primeira versão completos e aprovados |
| 5 — animações e áudio | Caminhada 4 direções, idle, FX, dado, vitória/derrota; seleção de música e sons | Continuidade visual e licenças/arquivos auditados |
| 6 — pacote de produção | Atlas, manifesto, prompts/origens, exportações e créditos | Auditoria de todos os assets; só agora começar implementação |
| 7 — motor local | Dado, grafo fixo, bifurcações, turnos, moedas e cristais usando arte aprovada | Uma partida completa sem HUD final, com integridade testada |
| 8 — experiência local | HUD final, eventos, negócios, itens, sabotagem, animação e som | Partida local 2–8 humanos completa |
| 9 — solo e persistência | Bots, dificuldades, save/load/exportação e inicializador Windows | 1 humano + bots, retomar partida e testar 8 assentos |
| 10 — balanceamento e acessibilidade | Simulações, partidas humanas, ajustes e celular | Duração medida, regras atualizadas, sem travamentos |
| 11 — online privado | Supabase e preview Vercel, salas e convite, autoridade e reconexão | Testes concorrentes e RLS aprovados; sem confiança no cliente |
| 12 — online público | Matchmaking, ausência, bots substitutos e controles de abuso | Teste de carga/custos e fluxo completo com 8 pessoas |
| 13 — lançamento | Build de produção, tutorial, créditos, monitoramento e checklist | Aprovação de publicação; rollback e backups conferidos |
| 14 — expansão | Novos tabuleiros, eventos e cosméticos | Dados de uso justificam; cada lote segue documentação → imagens → código |
Nenhuma etapa de sprite começa antes da aprovação do planejamento. Nenhuma implementação de jogo começa antes do pacote visual correspondente.

## Recomendações para aprovar
1. **Cinco cristais globais únicos**, não cinco por jogador; todos visíveis e coletáveis por passagem.
2. **Vitória imediata com os cinco**; clássico sem vencedor por dinheiro ou limite forçado de rodadas.
3. **Mapa fixo de 60 casas e cinco atalhos**, com cinco bairros de brinquedo.
4. **Sabotagem global antes do dado por 30 moedas e 2 PT**, derruba cristal aleatório e concede ao alvo proteção por uma oportunidade completa de reação.
5. **Dois pontos de tempo por turno**, com bico, ajuste de dado, itens e administração; não limitar movimento pelo trabalho.
6. **Negócios de renda leve**, no máximo dois por jogador; sem falência e sem eliminação.
7. **Pessoa segurando o carrinho de brinquedo nas mãos**, caminhando; oito cores com símbolos próprios.
8. **Miniaturas pintadas em vista oblíqua**, tudo em imagem gerada; texto real para HUD acessível.
9. **MVP sem minigames**, começando offline e com salas online privadas antes da fila pública.
10. **Áudio gratuito por seleção auditada**, priorizando CC0; candidatos ainda precisam de audição.
Nome “Expedição dos Cinco Cristais” é temporário e pode mudar sem alterar mecânicas.

## Fora do escopo inicial proposto
Minigames de ação, chat livre, voz, comércio entre jogadores, equipes, editor público de mapa, ranking competitivo, compras reais e monetização.
Offline não é multiplayer remoto: amigos em computadores diferentes chegam na etapa online.
A opção de jogar sozinho significa solo contra bots; modo treino isolado é secundário.

## Como registrar aprovação
O proprietário pode aprovar o pacote ou alterar pontos específicos. Registrar data, pontos aprovados, exceções e próxima etapa autorizada neste documento. Não interpretar entrega de documentação como aprovação automática.
Próxima ação recomendada após aprovação: fechar tabela das 60 casas e gerar conceitos, antes de qualquer código.

## Aprovação registrada — 28/10/2026
Usuário: “achei boa a organização e proposta, pode seguir”. Pacote de recomendações aprovado sem exceções; autorizado detalhar mapa e gerar conceitos. Exigências adicionais: sempre commit/push e manter AI_State atualizado. Revisão dos conceitos precede produção em escala, conforme roadmap.
