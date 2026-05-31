# Visão Geral

O MangaTypesetter é um editor desktop feito em C++/Qt para preparar páginas de mangá, webtoon e manhua para tradução e typesetting.

Ele organiza o trabalho em projetos próprios, com páginas importadas, layers de texto, máscaras, repintura, OCR, tradução e exportação final.

[Projeto aberto](../imagens/PrincipalProjetoAberto.png)

## Objetivo do App

O app foi pensado para reduzir o trabalho repetitivo no fluxo de tradução visual:

1. Importar imagens originais.
2. Detectar balões ou criar áreas de texto manualmente.
3. Gerar máscaras para remover texto original.
4. Enviar a área mascarada para repintura/inpainting.
5. Rodar OCR quando necessário.
6. Traduzir, revisar e aplicar texto.
7. Ajustar estilo, ordem e posicionamento.
8. Exportar páginas finais.

## Conceitos Principais

### Projeto

Um projeto guarda metadados, páginas, layers, vínculos e configurações de trabalho.

Arquivos principais:

* `.mtp`: metadados do projeto.
* `.mtchapter`: páginas, layers e dados do capítulo.

### Página

Cada página representa uma imagem original importada. A página pode conter layers por cima dela.

### Layer

Layer é qualquer elemento editável sobre a página.

Tipos principais:

* `ImageLayer`: imagem base/original.
* `TextLayer`: caixa de texto editável.
* `CleanupLayer`: limpeza manual retangular.
* `MaskLayer`: máscara usada para remover texto.
* `InpaintLayer`: resultado de repintura/inpainting.

### Modo Paginado

Mostra uma página por vez. É o modo tradicional de edição página a página.

### Modo Contínuo

Mostra várias páginas em sequência. É útil para leitura contínua, webtoon/manhua e casos em que uma seleção ou texto atravessa mais de uma página.

### Cross-Page

Recurso multi-página. Uma `TextLayer`, seleção, máscara ou repintura pode atravessar a divisão entre páginas, mas o resultado persistido deve continuar organizado por página.

## O Que Já Está Implementado

* Criação e abertura de projetos.
* Importação de imagens.
* Canvas Paginado e Contínuo.
* Painéis de páginas, layers, propriedades e automação.
* TextLayers com estilo, conteúdo, OCR e tradução.
* Máscara com OpenCV Server.
* OCR com MangaOCR, PaddleOCR e APIs configuráveis.
* Repintura com IOPaint, ComfyUI e APIs de edição configuráveis.
* Exportação em background para `export/`.
* Logs e trace por sessão.
* Painéis flutuantes de UI.

## Limitações Importantes

* Algumas automações ainda dependem de servidores locais Python.
* A qualidade de OCR, máscara e repintura depende muito da imagem, do modelo e do prompt.
* Recursos cross-page são mais complexos e devem ser testados em páginas reais.
* Undo/Redo ainda não cobre todos os fluxos avançados.

