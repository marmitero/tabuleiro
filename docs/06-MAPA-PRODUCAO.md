# Mapa e preparação de produção — v0.2

Atualização: 28/10/2026. Detalhamento da proposta aprovada; sem código de jogo.

## Fonte canônica
[casas-v0.2.csv](mapa/casas-v0.2.csv) lista os 60 IDs, tipo, setor lógico, coordenadas e saídas. São dados de planejamento; a implementação futura deverá importá-los sem reinventar o mapa.
Canvas de referência: 3072×2048, origem superior esquerda. Coordenadas são centros de casas, não posições dos pés. Ajustes artísticos devem preservar arestas e distâncias lógicas; versionar CSV se mudar coordenadas.
Rota padrão de bifurcações é a primeira saída no CSV (anel externo); segunda saída é atalho. Entre casas interpolar o movimento; não criar casas extras no caminho ilustrado.

## Bairros e caminhos
Cinco setores temáticos em sentido horário: 1 jardim de doces (C05–C12), 2 porto de brinquedos (C13–C20), 3 oficina mecânica (C21–C28), 4 feira luminosa (C29–C36), 5 praça do parque (C37–C40 e C01–C04).
Cada atalho parte do fim de um setor e atravessa uma faixa interna até o fim do seguinte. Sua coluna setor identifica o setor de saída, não uma regra de cristal.
Os cinco atalhos economizam três passos: substituem oito arestas por cinco. Não há travessia entre atalhos no centro. Uma interseção visual nunca cria conexão lógica.
Portais C16/C32 permitem teleporte opcional apenas pela regra correspondente. C01 é a partida compartilhada; sobreposição resolvida visualmente com oito posições ao redor.

## Casas e equilíbrio preliminar
boa: 14; evento: 8; loja: 4; negocio: 5; neutra: 4; pedagio: 4; portal: 2; ruim: 10; sorte: 4; trabalho: 5.
Atalhos A/B/D/E têm pedágio e casa ruim. F tem duas casas ruins. Isso representa o custo de encurtar o trajeto; o efeito só se aplica se parar na casa.
Todo negócio está no anel externo: sair para atalho pode custar oportunidade de renda ou coleta. Os atalhos não exigem pagamento de passagem; pedágio é casa final comum, não barreira.
Os nomes comerciais são decorativos: banca de doces C05, armazém de brinquedos C13, oficina C21, barraca de prêmios C29, quiosque C37. Todos têm mesmos valores.
Neutras: C01, C40, B4, F4. Não há prêmio automático por completar volta.

## Zonas iniciais dos cristais
| Cristal | Forma | Casas candidatas (sorteio uniforme) |
|---|---|---|
| CR01 | Gota facetada | C05, C06, C08 |
| CR02 | Cubo oblíquo | C13, C14, C18 |
| CR03 | Prisma longo | C21, C22, C26 |
| CR04 | Cluster de três pontas | C29, C30, C34 |
| CR05 | Octaedro | C37, C38, C39 |
Um cristal por conjunto, cinco sorteios independentes, sem casas repetidas. Cores de cristais serão escolhidas visualmente com destaque e contorno, sem depender exclusivamente delas para identidade.
Após sabotagem, qualquer casa elegível do mapa pode recebê-lo; não restringir à zona inicial. Distância de exclusão é a menor distância dirigida do jogador ao destino.

## Conferência estrutural realizada
- 60 IDs únicos, 65 arestas dirigidas e cinco bifurcações.
- Contagens por tipo conferidas contra o GDD.
- De qualquer uma das 60 casas, todas as demais são alcançáveis.
- Todas as 15 candidatas iniciais ficam a pelo menos quatro arestas de C01.
- Portais, partida, lojas e negócios têm IDs definidos.
Foi uma verificação estrutural por ferramenta temporária, não uma simulação de partidas. Economia e duração continuam sem medição.

## Instruções para conceitos gerados
Concept do tabuleiro é referência de materiais, câmera e atmosfera; não é arquivo final de colisão ou fonte de contagem de casas. A topologia exata permanece no CSV. Produção final deve separar chão, casas, conexões e decoração para posicionar imagens segundo o mapa.
Produzir agora três conceitos: mapa panorâmico sem HUD; personagem mestre coral segurando carrinho; HUD desktop com o tabuleiro e oito cartões.
Os três serão revisados visualmente e salvos com prompts, dimensões, hash e observações. Não iniciar oito cores/animações sem consolidar o mestre.
