# Máscara e Repintura

Máscara e repintura removem texto original da imagem e reconstruem o fundo.

## Fluxo Normal

1. Criar ou detectar uma `TextLayer`.
2. Gerar `MaskLayer`.
3. Enviar imagem + máscara para inpainting.
4. Criar `InpaintLayer`.
5. Conferir se o fundo ficou correto.

## MaskLayer

Indica a região que deve ser removida.

Formato visual esperado:

* branco: área afetada;
* preto/transparente: área preservada.

## InpaintLayer

Imagem resultante da repintura.

Ela deve representar apenas a área local vinculada à máscara/layer.

## Cross-Page

Em casos multi-página, o app pode montar um crop contínuo internamente.

Resultado persistido esperado:

```text
Página 13
├─ MaskLayer individual
└─ InpaintLayer individual

Página 14
├─ MaskLayer individual
└─ InpaintLayer individual
```

Mesmo que o processamento interno use uma imagem combinada, o usuário deve ver layers individuais por página.

## ComfyUI

Para usar ComfyUI:

1. importe um workflow API JSON;
2. configure nodes de imagem, máscara, prompt e saída;
3. revise os campos mapeados na API;
4. teste com uma área pequena.

Em Debug, o app salva payloads enviados ao ComfyUI em:

```text
<projectDir>/.debug/inpaint/
```

## Problemas Comuns

### Resultado usa imagem errada

Verifique se o workflow importado está usando o node correto de `LoadImage` e se o app está substituindo o campo configurado.

Use `.debug/inpaint` para conferir o JSON enviado.

### Máscara pega área errada

Confira:

* posição da `TextLayer`;
* crop salvo;
* arquivo de máscara;
* padding/safety margin;
* se o texto atravessa página.

### Resultado ruim no inpaint

Pode ser prompt, modelo, máscara muito grande, máscara muito pequena ou imagem de entrada errada.

