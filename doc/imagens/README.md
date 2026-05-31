# Imagens da Wiki

Use esta pasta para guardar screenshots e diagramas usados na documentação.

## Sugestão de Organização

```text
doc/imagens/
├─ usuario/
├─ fluxos/
├─ desenvolvimento/
└─ referencia/
```

## Convenção de Nomes

Use nomes descritivos:

```text
interface-principal.png
painel-layers-text-mask-inpaint.png
automacao-ocr.png
exportacao-progresso.png
modo-continuo-cross-page.png
trace-analyzer-output.png
```

## Como Substituir Placeholders

Troque:

```text
[AQUI VOCÊ ADICIONA A IMAGEM MOSTRANDO X NA PARTE Y]
```

por:

```markdown
![Descrição curta](../imagens/usuario/nome-da-imagem.png)
```

Use caminho relativo a partir do arquivo Markdown onde a imagem será exibida.

