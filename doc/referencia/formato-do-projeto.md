# Formato do Projeto

O formato do MangaTypesetter usa arquivos JSON com extensões próprias.

## `.mtp`

Arquivo de metadados do projeto.

Guarda:

* nome do projeto;
* template;
* idiomas;
* modo de visualização;
* path do capítulo;
* configurações relacionadas ao projeto.

## `.mtchapter`

Arquivo principal do capítulo.

Guarda:

* páginas;
* layers;
* vínculos;
* grupos;
* dados cross-page;
* campos de OCR/tradução;
* última página aberta.

## Página

Campos comuns:

* path da imagem original;
* nome de exibição;
* lista de layers;
* metadados de página.

## Layer Base

Campos comuns:

* `id`;
* `name`;
* `type`;
* `position`;
* `size`;
* `visible`;
* `locked`;
* `opacity`;
* `zIndex`.

## TextLayer

Campos adicionais:

* `sourceText`;
* `translatedText`;
* `text`;
* `fontFamily`;
* `fontSize`;
* `bold`;
* `italic`;
* `color`;
* `alignment`;
* `verticalAlignment`;
* `marginLeft`;
* `marginRight`;
* `strokes`;
* vínculos com máscara e inpaint;
* dados cross-page quando aplicável.

## MaskLayer

Campos adicionais:

* `maskPath`;
* `previewPath`;
* `parentTextLayerId`;
* `linkedTextLayerId`;
* `linkedInpaintLayerId`;
* `bbox`;
* `source`.

## InpaintLayer

Campos adicionais:

* `imagePath`;
* `sourceMaskLayerId`;
* `sourceTextLayerId`;
* `parentTextLayerId`;
* listas de origem quando há relação multi-layer.

## Compatibilidade

Ao alterar o formato:

1. manter leitura de campos antigos quando possível;
2. adicionar valores padrão seguros;
3. evitar quebrar projetos existentes;
4. registrar migrações no log;
5. atualizar esta página.

