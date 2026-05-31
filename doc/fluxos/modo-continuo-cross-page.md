# Modo Contínuo e Cross-Page

O modo Contínuo permite trabalhar com páginas em sequência, sem depender de uma página isolada.

[Canvas no modo Contínuo](../imagens/Cross-pageContínuos.png)

## Quando Usar

Use quando:

* o capítulo é webtoon/manhua;
* um balão ou texto atravessa páginas;
* você precisa selecionar uma área entre páginas;
* a leitura contínua ajuda a revisar ritmo e ordem.

## TextLayer Cross-Page

Uma `CrossPageTextLayer` representa uma caixa de texto que atravessa páginas.

Visualmente:

* deve aparecer como uma única caixa;
* deve ter um único frame;
* deve ter handles na caixa completa.

Internamente:

* mantém segmentos por página;
* usa coordenadas de cena contínua;
* exportação e persistência precisam decompor dados por página quando necessário.

## Seleção Cross-Page

Ferramentas que podem criar seleção multi-página:

* retangular;
* elíptica;
* laço livre;
* laço poligonal;
* varinha mágica.

O estado de seleção deve guardar:

* path global na cena contínua;
* segmentos locais por página.

## Varinha Mágica Cross-Page

Fluxo:

1. usuário clica em uma região;
2. o app faz seleção local;
3. se a seleção toca a borda superior/inferior, monta crop contínuo;
4. roda flood fill no crop contínuo;
5. divide o resultado por página.

## Máscara e Inpaint Cross-Page

O processamento pode usar imagem contínua temporária.

Mas o resultado final do projeto deve ser individual:

```text
Página A
├─ MaskLayer
└─ InpaintLayer

Página B
├─ MaskLayer
└─ InpaintLayer
```

## Cuidados

* Não transformar inpaint cross-page em uma única layer final visível.
* Não reconstruir painéis laterais durante scroll.
* Não renderizar texto pesado dentro de paint.
* Não trocar de página visualmente durante automações em lote.

