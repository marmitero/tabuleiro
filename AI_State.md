# AI_State — Expedição dos Cinco Cristais

Atualizado: 28/10/2026 (America/Sao_Paulo).

## Leia primeiro
Repositório canônico: https://github.com/marmitero/tabuleiro • branch main.
Este arquivo deve ser atualizado em toda entrega relevante. Fazer commit e push por marco; verificar sincronização antes de encerrar. Nunca afirmar que foi salvo no GitHub sem confirmação.
Ler este estado, README e documentos relevantes antes de retomar. Não usar memórias de outros jogos como requisito deste projeto.

## Aprovação e restrições
Usuário aprovou organização/proposta e autorizou seguir em 28/10/2026. Também exigiu commits/push contínuos e AI_State atualizado.
Aprovação abrange regras propostas, visual de miniaturas e pessoa segurando carrinho nas mãos. Nome continua provisório.
Ordem: documentação → imagens/sprites → código. Nenhum código de jogo ainda. Sem sprites em CSS ou arte procedural. Não criar Supabase/Vercel ainda; primeira versão offline.

## Etapa atual
Etapa 2 concluída estruturalmente; entrando na etapa 3: conceitos de mapa, personagem mestre e HUD via imagegen.

## O que temos
- README e cinco documentos originais de regras, arte/HUD, pesquisa/áudio, arquitetura e roadmap.
- Regras aprovadas: cinco cristais globais, coleta por passagem, sabotagem 30 moedas/2 PT, proteção e dois PT por turno, negócios limitados, oito assentos.
- docs/06-MAPA-PRODUCAO.md e docs/mapa/casas-v0.2.csv: 60 casas, coordenadas, tipos, 65 arestas, zonas iniciais.
- Validação estrutural de contagens, conectividade total e distância inicial dos cristais.

## O que falta
- Gerar e revisar três conceitos; registrar prompts e resultados, salvar imagens no repo.
- Consolidar personagem mestre; produzir oito cores, objetos, cenário, HUD, animações e FX.
- Ouvir/selecionar áudio gratuito, baixar e guardar licenças; shortlist existe, nenhum áudio incluído.
- Auditar todos os assets antes de iniciar código.
- Implementar local, bots, saves, testes/balanceamento; depois online privado/público.

## Retomada imediata
1. Conferir git status e main remoto.
2. Consultar docs/06-MAPA-PRODUCAO.md e Bíblia de arte.
3. Gerar conceitos com ferramenta nativa de imagens, inspecionar e preservar originais.
4. Atualizar inventário e este arquivo; commit/push das imagens e documentação.

## Verificação e limites
Somente estrutura de mapa verificada. Nenhuma simulação, jogo executável, imagem ou áudio produzido neste checkpoint.
Valores econômicos e duração são hipóteses. Concepts não substituem o mapa lógico.

## Histórico
- 28/10/2026: documentação inicial publicada (4055a19).
- 28/10/2026: aprovação recebida; mapa detalhado e este estado criados. SHA do checkpoint deve ser consultado no histórico git, evitando autorreferência.
