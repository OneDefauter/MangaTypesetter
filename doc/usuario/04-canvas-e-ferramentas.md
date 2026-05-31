# Canvas e Ferramentas

O canvas é a área de edição visual das páginas.

[Canvas e textleyer selecionada](../imagens/CanvasTextlayer.png)

## Modos de Canvas

### Modo Paginado

Mostra a página atual.

Use quando:

* estiver ajustando texto com precisão;
* estiver editando layers individuais;
* quiser desempenho previsível em páginas grandes.

### Modo Contínuo

Mostra páginas em sequência.

Use quando:

* estiver trabalhando com webtoon/manhua;
* precisar selecionar áreas entre páginas;
* precisar criar ou editar `CrossPageTextLayer`.

## Ferramentas Principais

### Seleção

Seleciona layers no canvas.

Com uma `TextLayer` selecionada:

* a caixa de seleção aparece;
* handles aparecem nos cantos e lados;
* arrastar o corpo move a layer;
* arrastar handles redimensiona.

### Texto

Cria `TextLayer`.

Fluxo:

1. Selecione a ferramenta de texto.
2. Arraste no canvas para criar a caixa.
3. Edite o texto no painel de Propriedades.
4. Ajuste fonte, tamanho, cor e stroke.

### Seleção Retangular

Cria uma seleção de área retangular.

Pode ser usada para:

* gerar máscara;
* OCR por seleção;
* ações futuras de limpeza.

### Seleção Elíptica

Cria seleção em formato de elipse.

### Laço Livre

Cria seleção com desenho livre.

### Laço Poligonal

Cria seleção por pontos.

### Varinha Mágica

Seleciona regiões semelhantes por cor.

No modo Contínuo, pode selecionar áreas cross-page quando a seleção toca a borda superior ou inferior de uma página.

[Cross-page em duas páginas](../imagens/VarinhaMágicaContínuo.png)

### Mão/Pan

Serve para mover a visualização.

Atalho:

* segure `Espaço` para ativar temporariamente;
* solte `Espaço` para voltar à ferramenta anterior.

### Zoom

Atalhos comuns:

* `Ctrl + Scroll`: aproximar/afastar.
* `Ctrl+0`: ajustar zoom.

## Backend do Canvas

Em Configurações, o canvas pode usar:

* `Raster padrão`;
* `OpenGL (experimental)`.

Use OpenGL apenas se o comportamento estiver bom no seu sistema. Se houver artefatos ou instabilidade, volte para Raster.

