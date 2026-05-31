# Debug de OCR e Inpaint

Em build Debug, o MangaTypesetter salva arquivos auxiliares dentro da pasta do projeto para facilitar inspeção.

## OCR

Pasta:

```text
<projectDir>/.debug/ocr/
```

Conteúdo esperado:

* imagem/crop enviado ao OCR;
* nome com data, página, layer e retângulo.

Use para responder:

* o crop está correto?
* o texto aparece inteiro?
* o app cortou parte do texto?
* o pré-processamento removeu algo importante?

## Inpaint

Pasta:

```text
<projectDir>/.debug/inpaint/
```

Conteúdo esperado:

* `_image.png`: imagem enviada;
* `_mask.png`: máscara enviada;
* `_prompt.txt`: prompt;
* `_meta.json`: metadados;
* `_comfy_request.json`: payload enviado ao ComfyUI;
* `_comfy_workflow.json`: workflow depois da injeção;
* `_comfy_meta.json`: mapeamento de nodes e campos.

## Como Conferir ComfyUI

1. Abra `_comfy_request.json`.
2. Confira se os nomes de imagem e máscara enviados são os arquivos atuais.
3. Abra `_comfy_workflow.json`.
4. Confirme se os nodes configurados foram substituídos.
5. Compare `_image.png` e `_mask.png` com o resultado recebido.

## Quando Usar

Use essa pasta sempre que:

* OCR retorna texto errado;
* inpaint usa imagem errada;
* prompt parece não ser aplicado;
* máscara enviada não corresponde à seleção;
* ComfyUI usa imagem antiga do workflow.

