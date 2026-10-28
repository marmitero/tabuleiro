# Bíblia de arte, HUD e produção de imagens — v0.1
Status: direção proposta, aguardando aprovação. Nenhuma imagem gerada nesta etapa.
Aplicar skill imagegen na produção: imagem gerada de verdade, fundo transparente quando necessário, inspeção visual antes de aceitar.

## Direção visual
2D com aparência de miniaturas 3D pintadas, vista superior oblíqua fixa (aproximadamente 35 graus), volumes arredondados, contornos discretos, luz suave do alto à esquerda e sombras curtas.
Tabuleiro colorido em parque de brinquedos; piso menos saturado que personagens e cristais. Evitar excesso de decoração sobre casas.
Não copiar personagens, silhuetas, mapas ou HUD das referências.
Recomendação para “carregando”: pessoa caminhando e segurando o carrinho de brinquedo nas mãos, à frente do corpo, com cristais visíveis nele. Não presumir que a pessoa dirige ou empurra o carrinho; confirmar essa leitura antes da folha de personagem.

## Política de imagens
Todo elemento artístico do jogo vem de arquivos raster gerados: cenário, caminhos, casas, personagens, carrinhos, moedas, cristais, dado, ícones, molduras e efeitos.
Sem emojis como assets, desenhos CSS, ícones de biblioteca ou formas procedurais substituindo arte. CSS permitido para layout, tipografia acessível, posicionar e animar imagens existentes.
Canvas/WebGL permitido para compor sprites e movimentá-los; não para desenhar substitutos artísticos. Brilhos/confetes usam imagens geradas, inclusive partículas.
Texto de botão, valores e textos longos são texto real sobre molduras raster; não gravar textos na imagem gerada. Áreas de clique e indicadores de foco acessível são elementos funcionais, não sprites.
Mapa e grafo fixos feitos à mão; apenas dado, cartas e posições elegíveis de cristais são sorteados.

## Oito identidades
| Assento | Cor de destaque | Código | Símbolo adicional |
|---|---|---|---|
| 1 | Vermelho coral | #E64B52 | Círculo |
| 2 | Azul royal | #376DE8 | Triângulo |
| 3 | Verde folha | #279B60 | Folha |
| 4 | Amarelo ouro | #F2C438 | Sol |
| 5 | Roxo violeta | #8752CE | Lua |
| 6 | Laranja | #EC822E | Raio |
| 7 | Rosa magenta | #D94BA2 | Flor |
| 8 | Ciano turquesa | #24B9C7 | Gota |
Cor no carrinho, roupa e placa do jogador; contorno claro/escuro para separar do chão.
Cada símbolo também deve ser imagem gerada e aparecer na HUD e junto do personagem. Testar em escala de cinza e simulações de daltonismo.
Primeiro aprovar uma pessoa e carrinho mestre; depois derivar as oito variantes preservando escala, câmera e proporções.

## Especificações propostas
- Master do mapa: 3072×2048 ou maior, com exportação em camadas/trechos para carregamento; dimensões finais validadas antes da geração.
- Personagem: células finais 256×256, pivô nos pés em (128,224), área segura de 16 px; exibição aproximada 64–96 px conforme zoom.
- Casas: 256×256; ícones: 128×128; cristais/moedas/itens: 128×128.
- FX: células 256×256; vitória/derrota: 512×512.
- Molduras: PNG transparente em nove partes ou nove recortes raster; fundos de painel em resolução suficiente para desktop.
- PNG RGBA como master aprovado; WebP para distribuição quando preservar alpha e qualidade; não comprimir masters destrutivamente.
- Atlases limitados inicialmente a 2048×2048, padding 4 px e extrusão de borda; manifesto de frames, duração, pivô, escala, versão e origem.
- Não esperar que imagegen entregue grade temporal perfeita. Produzir frames com referência mestre, recortar/alinha-los tecnicamente e revisar tremor, transparência e continuidade; regenerar frames inconsistentes.
- Corte, redução, alinhamento e montagem de atlas não substituem a criação de arte por imagens geradas.

## Inventário de animações
| Asset | Estados/frames finais previstos | Observação |
|---|---|---|
| Cada personagem | Parado 4 direções × 4; caminhada 4 × 8 | 48 frames por cor, 384 para as oito cores |
| Cada personagem | Coleta 6; comemoração 8; derrota 6; susto 4 | 24 por cor, 192 no total; direção frontal oblíqua basta nesses estados |
| Carrinho | Integrado aos frames da pessoa | Não flutuar nem mudar de tamanho |
| Dado | 12 frames girando + 6 faces finais | Resultado definido pela regra, imagem apenas apresenta |
| Cristais | 5 formatos × 8 frames de brilho | Não confundir com cores de jogador |
| Moeda | 8 frames de rotação | Ícone estático reutiliza um frame |
| FX | 9 famílias × 8 frames | Ganho/perda de moeda, coleta, boa, ruim, sabotagem, escudo, vitória, derrota |
| Ambiente | 5 famílias × 4 frames | Água, bandeiras, luzes, folhas e mecanismo da oficina |
Subtotal de personagens: 576 frames previstos; contagem é orçamento inicial e pode mudar após teste visual.
Animação de movimento percorre arestas com aceleração suave, passos e balanço do carrinho; não apenas deslizar sprite parado.
Movimento 250–400 ms por casa; dado 700–1000 ms; efeitos comuns 500–900 ms; coleta 1000–1400 ms; vitória 2500–4000 ms.
Permitir acelerar animações, movimento reduzido e pular vinhetas; apresentar sempre o resultado textual.

## HUD e telas
1. Menu: jogar local, futuro jogar online, tutorial, configurações e créditos.
2. Configuração: assentos 1–8, humano/bot/dificuldade, cores únicas, semente opcional, áudio e acessibilidade.
3. Online futuro: criar sala, entrar por código, pronto, convites, conexão e preenchimento por bot.
4. Mesa: tabuleiro ocupa maior área; faixa superior com rodada e ordem dos jogadores; oito cartões compactos de saldo/cristais.
5. Jogador ativo: retrato, símbolo, moedas, 2 PT, 5 espaços de cristal e três slots de item.
6. Ações inferiores: preparar, item, sabotar, dado e encerrar quando aplicável; botão indisponível explica motivo.
7. Bifurcação: setas em imagem, destaque de destinos, passos restantes e prévia de custo/risco; confirmação por toque/teclado.
8. Seleção de sabotagem: alvo, cristais, proteção, escudo, preço e consequência antes de confirmar.
9. Loja/negócio/evento: painel com preço, saldo após ação, efeito e opção de recusa.
10. Histórico: últimos acontecimentos, expansível; resultado do dado e ganhos/perdas também em texto.
11. Pausa: salvar/carregar offline, som/música separados, velocidade, movimento reduzido e sair.
12. Vitória: vencedor com cinco cristais, estatísticas e revanche; demais jogadores recebem animação de derrota amistosa.
No desktop, histórico e detalhes laterais. No celular, cartões compactos e painel inferior recolhível, zoom por pinça, recentralizar jogador e mapa panorâmico. Não exigir hover.
Meta: controles de pelo menos 44×44 px, texto de corpo a partir de 16 px, leitura em 360 px de largura, teclado e foco visível.
A estética da HUD usa molduras geradas; textos continuam traduzíveis e acessíveis.

## Lotes e aprovação de produção
A. Concept do mapa e mockup visual da HUD; pessoa/carrinho mestre, cinco cristais, moeda e dado.
B. Oito cores e folha de direções; somente avançar após identidade e leitura aprovadas.
C. Cenário fixo, pisos, caminhos, 10 tipos de casa, cinco negócios, lojas, portais e decoração.
D. Molduras, botões normal/hover/pressionado/desabilitado, ícones e painéis.
E. Animações completas e FX; revisão quadro a quadro e em reprodução.
F. Exportações otimizadas, atlas e manifesto; auditoria antes de código.
Toda arte usada na primeira implementação deve estar produzida e aprovada previamente. Novo escopo exige documentação → arte → código.

## Prompt mestre de produção
“Asset original para jogo de tabuleiro de navegador em parque de brinquedos; miniatura pintada, 2D com volume 3D, vista oblíqua fixa, luz do alto à esquerda, cores alegres, silhueta legível em tamanho pequeno. [SUJEITO E ESTADO]. Mesma câmera, escala, materiais e proporções da referência mestre aprovada. Sem letras, números, logos ou marcas d'água. [FUNDO TRANSPARENTE quando sprite isolado]. Manter margens, pivô e objeto inteiro.”
Prompt de personagem: explicitar pessoa segurando pequeno carrinho nas mãos e direção da caminhada; não gerar um carro dirigido por pessoa.
Prompt de cenário: reservar áreas das 60 casas conforme mapa desenhado e não incorporar casas com texto ou contagem imprecisa. Gerar cenário em camadas e montar sobre coordenadas aprovadas.
Registrar prompt completo e imagens de referência por asset, não apenas este modelo.

## Critérios de aceite
Sem halos/fundo quadriculado pintado; carrinho consistente; oito identidades distinguíveis; cinco formatos de cristal; contagem de frames correta; ausência de texto falso; cenário não oculta rotas; pivôs sem tremor; FX não bloqueia decisão; leitura aprovada em desktop e celular.
Organização futura: assets/source, assets/approved, public/assets/{board,characters,ui,fx,audio}; ASSET-MANIFEST e CREDITS com origem, versão, autor/ferramenta e licença aplicável.
