# Glossário Técnico

## Canvas

Área visual onde a página e suas layers são editadas.

## Modo Paginado

Modo de edição que mostra uma página por vez.

## Modo Contínuo

Modo de edição que mostra páginas em sequência, usado para leitura contínua e recursos cross-page.

## Cross-Page

Recurso que atravessa mais de uma página.

Exemplo:

* seleção entre páginas;
* TextLayer entre páginas;
* máscara/inpaint gerados a partir de crop contínuo.

## Layer

Elemento editável sobre a página.

## TextLayer

Layer de texto.

Guarda OCR, tradução, texto aplicado e estilo visual.

## MaskLayer

Layer de máscara.

Define a área que será removida ou repintada.

## InpaintLayer

Layer com resultado de repintura.

## CleanupLayer

Layer de limpeza manual.

## OCR

Reconhecimento óptico de caracteres.

Extrai texto visível de uma imagem/crop.

## Inpainting

Processo de reconstruir uma área da imagem, geralmente após remover texto.

## Trace

Arquivo `.mtrace` em JSONL com eventos de performance.

## Jank

Travada perceptível na UI, geralmente causada por operação longa na thread principal.

## LOD

Level of Detail. Estratégia para usar versões mais leves em zoom baixo.

## Cache de Texto

Imagem renderizada de uma TextLayer para evitar recalcular fonte/path/stroke a cada paint.

## Preview Leve

Renderização rápida e simplificada de texto usada para feedback imediato.

## ComfyUI Workflow API

JSON de workflow usado pelo ComfyUI para receber imagem, máscara, prompt e gerar saída.

## `.debug/ocr`

Pasta de debug onde crops enviados ao OCR são salvos em build Debug.

## `.debug/inpaint`

Pasta de debug onde entradas e payloads de inpaint são salvos em build Debug.

