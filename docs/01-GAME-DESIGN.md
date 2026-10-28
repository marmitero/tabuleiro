# Game Design Document — v0.1
Status: proposta para aprovação. Todos os valores numéricos adicionais são hipóteses de balanceamento, não resultados de testes.

## 1. Requisitos definidos pelo usuário
- Jogo de navegador, futuramente online com GitHub, Vercel e Supabase; primeira versão local offline.
- 1–8 humanos, humanos com bots e partidas online públicas; solo contra bots.
- Dado e deslocamento por casas, com premiações, efeitos e punições.
- Múltiplos caminhos escolhidos durante a partida.
- Vencer reunindo cinco cristais. Pagar moedas para derrubar um cristal adversário; ele reaparece em casa aleatória disponível.
- Visual colorido e animado, inteiramente baseado em imagens geradas; sem sprites construídos em CSS.
- Pessoa carregando carrinho de brinquedo, em oito cores bem diferenciadas.
- Efeitos de movimento, dado, moedas, cristal, casas boas/ruins e resultados.
- Documentar antes de gerar sprites; produzir sprites antes de programar.

## 2. Fantasia e pilares propostos
Nome provisório: Expedição dos Cinco Cristais.
Um parque de miniaturas de brinquedo dividido em bairros. Os competidores carregam pequenos carrinhos como recipientes das conquistas.
Pilares: leitura imediata; sorte com decisões relevantes; economia acessível; rotas disputadas; recuperação sem eliminação; espetáculo rápido.
Arte original com atmosfera de brinquedos pintados e aventura amigável. Interface e textos em pt-BR.
Sem combate de reflexo ou minigames na primeira versão.

## 3. Modos e participantes
- Solo: 1 humano + 1–7 bots; padrão sugerido de 3 bots.
- Local compartilhado: 2–8 humanos no mesmo computador, com bots opcionais.
- Sala online privada: 2–8 participantes totais, convite e bots opcionais.
- Online público: fila casual, 2–8 participantes, lançamento posterior.
- Limite de 8 assentos contando humanos e bots; 1 humano sem bot pode ser treino, sem vitória competitiva.
- Bots fácil, normal e difícil. Todos seguem as mesmas regras e não conhecem sorteios futuros.
- Sem vantagens de atributos entre as oito cores na primeira versão.

## 4. Tempo, recursos e economia
Recursos: moedas, dois pontos de tempo (PT) por turno, itens e cristais.
Moedas iniciais: 20. Moedas nunca negativas; sem dívida e sem eliminação por falência.
PT representam preparação e administração: renovam para 2 no início do turno, não acumulam.
Antes do dado, escolher até duas ações respeitando custos e limites:
| Ação | Custo | Resultado |
|---|---|---|
| Bico | 2 PT | +6 moedas; pode mover normalmente depois |
| Preparar carrinho | 1 PT + 4 moedas | +1 ou -1 no dado deste turno, escolhido após sorteio, resultado mínimo 1 e máximo 6 |
| Usar item | 1 PT | Um item; máximo um por turno |
| Sabotar | 2 PT + 30 moedas | Derruba um cristal de alvo elegível |
| Administrar negócio | 2 PT + 12 moedas | Melhorar um negócio próprio estando na casa dele |
Sem ação obrigatória: economizar moedas é uma decisão válida. Comprar na loja ou adquirir negócio é resolução da casa, sem PT, uma compra por parada.
A recomendação separa tempo estratégico de cronômetro: offline sem limite; online 45 s para preparação e 15 s por bifurcação ou escolha de evento, configuráveis em sala privada.
Ao expirar: sem compra/sabotagem, dado automático e rota padrão marcada. Ação já confirmada não é refeita.

## 5. Turno e rodada
Turno: vez de uma pessoa. Rodada: todos os assentos jogaram uma vez.
Ordem inicial sorteada uma vez; mantida. Um dado justo de seis faces por turno; sem turno extra ao tirar 6.
1. Renovar PT, aplicar manutenção e expiração de proteção.
2. Preparação: ações, alvos e custos explícitos.
3. Sortear dado e aplicar eventual ajuste comprado.
4. Animar movimento casa por casa; na bifurcação, escolher próximo caminho com movimentos restantes.
5. Ao atravessar ou parar em cristal, coletá-lo gratuitamente.
6. Na casa final, resolver seu efeito; casas intermediárias não ativam efeito comum.
7. Após cada coleta, verificar cinco cristais; vitória imediata tem precedência e encerra efeitos restantes.
8. Encerrar turno. Ao completar rodada, rendas e evento global previsto.
Todo deslocamento forçado resolve no máximo um novo efeito comum; não gerar cadeias infinitas.
Teleporte não coleta casas intermediárias. Cristal no destino é coletado.
Casa ocupada permite coexistência; personagens recebem deslocamento visual para não se sobrepor.

## 6. Tabuleiro proposto
Um mapa fixo feito à mão, com 60 casas e cinco bairros ligados por bifurcações e atalhos. Topologia proposta, ainda sem arte ou coordenadas finais.
Estrutura: anel externo de 40 casas (C01–C40), conexões de C40 para C01; cinco atalhos internos de 4 casas cada:
C04 → A1 → A2 → A3 → A4 → C12;
C12 → B1 → B2 → B3 → B4 → C20;
C20 → D1 → D2 → D3 → D4 → C28;
C28 → E1 → E2 → E3 → E4 → C36;
C36 → F1 → F2 → F3 → F4 → C04.
As saídas do anel mantêm também a rota externa; grafo dirigido, sem retorno imediato ou voltar passos voluntariamente. C01 é partida.
Atalhos trazem risco/custo; caminhos externos trazem oportunidades econômicas. Escolha mostra custo, destino e cristais adiante, sem revelar sorteios.
Bairros: praça central, jardim de doces, porto de brinquedos, oficina mecânica e feira luminosa.
Ciclo visual manhã/tarde/noite a cada quatro rodadas; cosmético no início. Evento global a cada três rodadas, anunciado com uma rodada de antecedência.
Distribuição de casas, soma 60:
| Tipo | Quantidade | Regra base |
|---|---:|---|
| Boa | 14 | +6 moedas |
| Ruim | 10 | -5 moedas, limitado ao saldo |
| Evento | 8 | Escolha ou carta de evento |
| Trabalho | 5 | Escolher +8 moedas ou pagar 4 para obter um item comum sorteado |
| Negócio | 5 | Compra e renda |
| Loja | 4 | Comprar um item |
| Pedágio | 4 | Pagar 3 moedas, limitado ao saldo |
| Sorte | 4 | Sortear prêmio de 4/8/12 moedas, pesos iguais |
| Portal | 2 | Teleporte opcional pago: 5 moedas até o outro portal; sem recursão |
| Neutra/partida | 4 | Sem efeito comum |
Antes da arte final, atribuir cada tipo aos 60 IDs e testar acessibilidade e distribuição; não programar sem esse registro aprovado.

## 7. Cristais: regra central e casos extremos
Interpretação recomendada: **exatamente cinco cristais únicos no jogo inteiro**, todos podem pertencer ao mesmo jogador. Não são cinco cópias por pessoa.
Cada cristal tem identidade e formato distintos; a mesma cor do jogador nunca é o único identificador.
Início: um cristal por bairro, em casa elegível; não na partida. Posições sorteadas de conjuntos predefinidos e publicamente visíveis. Para reduzir viés, posições iniciais devem ficar a pelo menos 4 arestas dirigidas de C01.
Cada cristal está exatamente em um estado: no mapa ou com um jogador. Nunca destruído, duplicado ou vendido.
Coleta por passagem para não exigir sorteio exato. No máximo um cristal por casa.
Coletou quinto: vence imediatamente; não há janela de sabotagem após a vitória.

### Sabotagem proposta
Disponível globalmente antes do dado: 30 moedas + 2 PT; alvo tem ao menos um cristal e não está protegido.
Escolher adversário; o cristal derrubado é sorteado uniformemente entre os dele. Atacante não recebe o cristal.
Custo debitado somente depois de validar alvo e destino; uma operação atômica no futuro online.
Destino escolhido uniformemente entre casas sem cristal, sem jogador, alcançáveis por todos e diferentes da partida e dos dois portais; excluir casa de origem e casas a menos de 3 arestas de qualquer jogador.
Se não houver destino com distância mínima, relaxar só essa distância; demais exclusões permanecem. O mapa de 60 casas e 8 participantes garante candidatos, mas falha de mapa deve cancelar ataque sem custo.
O alvo recebe proteção até o início de seu segundo próximo turno: tem uma vez completa para reagir antes de poder sofrer outro ataque.
Cristais novos/coletados não dão imunidade por si. Proteção não bloqueia perder moedas.
Escudo, se ativo: bloqueia um ataque, é consumido; atacante paga 10 moedas e 2 PT, em vez de 30. A existência do escudo é pública antes de confirmar.
Nunca é possível atacar a si mesmo. Alvo com zero cristais não aparece na seleção.
Motivo: permitir disputa sem roubo direto ou ataques repetidos ao mesmo alvo. Preço e proteção exigem testes.

## 8. Negócios, lojas e itens
Negócio custa 12 moedas; limite de dois por jogador; renda +2 por rodada.
Melhoria custa 12 moedas e 2 PT na própria casa; apenas um nível; renda passa a +3.
Adversário que parar paga 3 ao dono, limitado ao saldo; não toma negócio.
Venda voluntária antes do dado, sem PT: recebe 6 moedas, remove propriedade e melhoria. Uma venda por turno.
Negócios sem dono não obrigam compra. Renda começa no fechamento da rodada da compra.
Inventário: três itens; loja deve bloquear compra ou oferecer substituição explícita sem reembolso.
| Item | Preço | Efeito |
|---|---:|---|
| Escudo | 18 | Ativar por 1 PT; dura até bloquear ataque ou por duas rodadas; sem empilhar |
| Dado guiado | 10 | Usar por 1 PT: rolar duas vezes e escolher um resultado |
| Vale-pedágio | 6 | Usar por 1 PT: isenção de pedágio e aluguel até acabar o turno |
| Bússola | 8 | Usar por 1 PT: +2 passos neste turno, máximo 8 após ajustes |
Escudo e dado guiado podem combinar com preparar carrinho, respeitando 2 PT; dois itens no mesmo turno não.
Todas as lojas vendem os quatro itens, sem estoque global na primeira versão.

## 9. Catálogo inicial de eventos
Cartas de evento em baralho sem reposição; embaralhar descarte quando esgotar. Conteúdo visível antes de confirmar escolhas.
| ID | Evento | Resolução |
|---|---|---|
| EV01 | Entrega expressa | +8 moedas |
| EV02 | Roda emperrada | -6 moedas |
| EV03 | Feira de troca | Pagar 5 por um item comum sorteado, ou recusar |
| EV04 | Bico de última hora | +5 moedas e -1 passo no próximo turno, mínimo 1 |
| EV05 | Atalho da oficina | Avançar 3 passos, escolhendo bifurcações, ou ficar |
| EV06 | Chuva de confetes | Todos ganham 3 moedas |
| EV07 | Reparo coletivo | Todos perdem até 3 moedas |
| EV08 | Patrocínio | Quem tem menos cristais ganha 6; empate premia todos empatados |
| EV09 | Cashback | Recuperar até 5 moedas de compras desta rodada; se nenhuma, +2 |
| EV10 | Achados e perdidos | Receber um item comum ou +4 moedas se inventário cheio |
| EV11 | Passeio turístico | Teleportar gratuitamente para um dos dois portais ou recusar |
| EV12 | Escolha prudente | Receber 4 garantidos ou sortear 0/10 com chances iguais |
Item comum: dado guiado, vale-pedágio ou bússola, probabilidades iguais.
Evento EV05 não ativa novo efeito comum se já for deslocamento encadeado; cristais continuam coletáveis.
Globais, a cada 3 rodadas, alternados em baralho: renda extra +1 por negócio, lojas com desconto de 2 (mínimo 1), casas boas +2. Cada modificador dura só a rodada anunciada, sem acumular.

## 10. Duração, recuperação e fim
Meta inicial de duração: 25–45 minutos com 2–4 assentos; com 8, 45–75 minutos. São metas, ainda não medidas.
Sem limite obrigatório no modo clássico: só vence quem detém os cinco. Aos 30 ciclos completos, oferecer continuar, salvar ou encerrar sem vencedor; moedas não substituem a condição exigida.
Modo rápido com cristais por jogador ou vitória por pontuação seria outro regulamento e não está aprovado.
Em zero moedas: dado e coleta permanecem livres, bico oferece recuperação; sem perder turno inteiro como punição.
Dois turnos online consecutivos ausentes: bot temporário; reconexão devolve controle apenas na preparação do próximo turno. Desistência não apaga cristais: bot assume.
Se todos os humanos saírem, suspender sala e persistir estado; expiração de sala a definir antes do online.
Sem troca direta de cristais ou moedas entre participantes no MVP, para reduzir combinações contra terceiros.

## 11. Bots e equilíbrio
Fácil: rota legal aleatória com preferência ocasional por cristal; usa itens de forma simples.
Normal: estima distância a cristais, renda, risco e custo de sabotagem.
Difícil: considera disputa de rotas e chance de o líder vencer; sem bônus de moeda ou dado manipulado.
Medir duração, turnos sem decisão, saldo mediano, frequência de sabotagem, cristais por assento e vantagem da ordem inicial.
Testar especialmente concentração 4–1 de cristais, alvo sem dinheiro, cinco cristais em posse, 8 jogadores e efeito de renda acumulada.
Objetivo de ajuste: decisões de rota frequentes, bico útil sem superar todos os negócios, sabotagem relevante sem impedir conclusão.
