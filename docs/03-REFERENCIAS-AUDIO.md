# Pesquisa de referências e áudio
Consulta: 28/10/2026. Pesquisa documental em páginas oficiais e catálogos; não foi realizada sessão de jogo, audição crítica ou teste dos pacotes. Referência não equivale a licença para copiar.

## Jogos e aplicação ao projeto
| Fonte | Observação apoiada pela fonte | Aplicação original proposta |
|---|---|---|
| [Monopoly — Hasbro](https://instructions.hasbro.com/en-us/instruction/monopoly-board-game-classic-game-with-storage-tray-and-larger-tokens-family-games-8) | Comprar propriedades e receber aluguéis estruturam a economia | Cinco negócios de renda moderada; sem falência ou eliminação |
| [Jogo da Vida — manual Hasbro](https://www.hasbro.com/common/instruct/life.pdf) | Rotas de carreira, pagamentos e categorias de casas criam escolhas | Tempo de preparação, trabalho, eventos e trajetos com oportunidades diferentes |
| [Mario Party Jamboree — Nintendo](https://www.nintendo.com/us/store/products/super-mario-party-jamboree-switch/) | Dado, tabuleiro, moedas, estrelas e eventos sustentam a disputa | Cristais públicos, bifurcações, efeitos curtos e sabotagem que devolve objetivo ao mapa |
As páginas não determinam nosso regulamento: números, proteção e negócios neste projeto são propostas próprias.
Não incluir minigames inicialmente: priorizar o tabuleiro e reduzir espera entre oito participantes.

## Pacotes de referência para estudar arte
| Pacote/fonte | Estudar | Uso previsto |
|---|---|---|
| [Kenney Board Game Pack](https://kenney.nl/assets/boardgame-pack) | Legibilidade de dado, fichas, cartas e estados | Referência de escala e separação, sem substituir arte própria |
| [Kenney Board Game Info](https://kenney.nl/assets/board-game-info) | Comunicação visual de regras e ícones | Referência para HUD |
| [Kenney Playing Cards Pack](https://kenney.nl/assets/playing-cards-pack) | Consistência e organização de conjuntos | Referência para cartas de evento |
| [Kenney Nature Kit](https://kenney.nl/assets/nature-kit) | Volumes simples e grupos de vegetação | Referência de miniaturas; pacote 3D não será incorporado como sprite final |
| [Kenney City Kit Roads](https://kenney.nl/assets/city-kit-roads) | Junções, curvas e continuidade de rotas | Referência estrutural, não mapa copiado |
Fontes do Kenney identificam esses pacotes como CC0. O [suporte oficial](https://kenney.nl/support) informa que assets das páginas são CC0 e atribuição não é obrigatória.
Algumas aberturas diretas do catálogo falharam no mecanismo de consulta; metadados foram encontrados nas páginas oficiais indexadas. Arquivos não foram baixados ou auditados.
Antes da produção: consultar previews, montar comparativo visual e fechar câmera/escala com concept próprio. Não alegar inspeção quadro a quadro destes pacotes nesta etapa.

## Trilha e sons gratuitos: shortlist
| Fonte | Licença declarada | Candidato a uso | Pendência |
|---|---|---|---|
| [Kenney Interface Sounds](https://kenney.nl/assets/interface-sounds) | CC0 | Botões, navegação e confirmação | Ouvir, selecionar arquivos e ajustar volume |
| [Kenney UI Audio](https://kenney.nl/assets/ui-audio) | CC0 | Alternativa para HUD | Comparar com Interface Sounds e evitar mistura incoerente |
| [Kenney Music Jingles](https://kenney.nl/assets/music-jingles) | CC0 | Vitória, derrota e conquista | Ouvir e escolher timbres compatíveis |
| [A New Day — SpiderDave](https://opengameart.org/content/a-new-day) | CC0 na página do autor | Candidata à música de mesa/menu | Audição, verificação de loop e teste de fadiga |
| [Happy Adventure (Loop) — TinyWorlds](https://opengameart.org/content/happy-adventure-loop) | CC0 na página | Alternativa alegre chiptune | Estética retro pode destoar das miniaturas; ouvir antes de escolher |
| [Incompetech](https://incompetech.com/music/royalty-free/licenses/) | Opção gratuita com atribuição | Alternativa para trilha mais acústica | Selecionar faixa e guardar termos/crédito específico |
Incompetech não é uma indicação de domínio público. A [FAQ](https://apps.incompetech.com/music/royalty-free/faq.html) descreve crédito em jogos e atribuição CC BY 4.0; conferir a licença da faixa escolhida.
Nenhuma faixa está aprovada ou incluída. “Gratuito” não dispensa registrar os termos de cada arquivo. Mesmo para CC0, manter autor e origem nos créditos.

## Direção sonora proposta
Música instrumental alegre, sem voz; percussão leve, marimba, pizzicato e sinos suaves. Meta de 90–120 BPM para novas seleções; as faixas citadas ainda não foram medidas.
Três estados desejados: menu acolhedor, tabuleiro com loop pouco cansativo, tensão leve quando alguém possui quatro cristais. Pode começar com uma faixa de mesa e jingles.
Não usar áudio extraído de Monopoly, Jogo da Vida ou Mario Party.

| Evento | Som desejado |
|---|---|
| Passos/carrinho | Passos curtos e rodas discretas, sem repetição agressiva |
| Dado | Chocalho e impacto curto sincronizados |
| Moedas + / - | Escala ascendente / descendente, distinguíveis |
| Cristal | Brilho cristalino e acorde curto |
| Casa boa / ruim | Confirmação alegre / percussão grave leve |
| Sabotagem / escudo | Whoosh + queda / barreira suave |
| Vitória / derrota | Jingle festivo / encerramento amistoso |
| Turno e escolha | Notificação curta com alternativa visual |
Banco mínimo: 16 sons, uma música de mesa, uma de menu opcional e dois jingles.
Implementação futura: desbloquear áudio após gesto do usuário; volumes separados para música/FX; mute persistido; atenuar música nos eventos; limitar vozes simultâneas e frequência de moedas/passos.
Guardar WAV/OGG originais e exportar formatos compatíveis com navegadores alvo após teste. Loop sem estalo; evitar clipping; normalizar por percepção e testar em celular.
Registro obrigatório: título, autor, URL de origem, URL/licença e versão, data de download, nome original, alterações e hash. Preservar licença junto ao arquivo.

## Fontes técnicas para o planejamento futuro
- [Supabase Realtime](https://supabase.com/docs/guides/realtime): Broadcast, Presence e Postgres Changes. Transporte não substitui autoridade das regras.
- [Vercel Functions Limits](https://vercel.com/docs/functions/limitations): funções possuem limites de execução; não planejar uma partida inteira como processo residente de uma função.
Antes de implementar integrações, revisar documentação/changelog vigente, planos, limites e custos reais. Não foram criados serviços nesta fase.
