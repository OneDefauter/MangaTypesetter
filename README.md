# MangaTypesetter

MangaTypesetter é um editor desktop voltado para tradução, limpeza, redesenho e typesetting de páginas de mangá, webtoon e manhua.

A ideia do aplicativo é reunir em um único fluxo as etapas mais comuns de preparação de capítulos: importar páginas, detectar áreas de fala, executar OCR, revisar texto, gerar máscaras, limpar ou repintar balões, aplicar o texto traduzido e exportar o resultado final.

O projeto ainda está em desenvolvimento ativo. Algumas funções já fazem parte do fluxo principal, enquanto outras ainda são experimentais ou estão em evolução.

## Objetivo

O MangaTypesetter foi pensado para facilitar o trabalho de edição e tradução de capítulos completos, evitando que cada página precise ser tratada como uma imagem isolada.

O aplicativo trabalha com um projeto de capítulo, mantendo páginas, textos, máscaras, repinturas, estilos e informações de tradução organizados em um único fluxo.

Principais objetivos:

- importar e organizar páginas de mangá, webtoon e manhua;
- detectar balões e áreas de fala;
- criar áreas de texto manualmente;
- executar OCR em áreas selecionadas ou páginas inteiras;
- gerar máscaras para limpeza de texto;
- usar inpainting/repintura para remover texto original;
- aplicar texto traduzido com controle de estilo;
- revisar a ordem de leitura dos balões;
- exportar páginas ou capítulos finalizados.

## Fluxo principal

O fluxo esperado para uma página é:

1. Importar as páginas do capítulo.
2. Detectar balões automaticamente ou criar áreas de texto manualmente.
3. Criar uma camada de texto para cada fala ou área detectada.
4. Gerar máscara para a região do texto original.
5. Aplicar limpeza ou inpainting na área mascarada.
6. Rodar OCR quando necessário.
7. Revisar o texto original, a tradução e o texto aplicado.
8. Ajustar fonte, tamanho, cor, contorno, alinhamento, posição e rotação.
9. Organizar a ordem de leitura.
10. Exportar a página ou o capítulo finalizado.

As relações principais do fluxo são:

```text
TextLayer
├─ MaskLayer
└─ InpaintLayer
```

Também há suporte inicial a grupos de mesclagem, onde dois ou mais textos continuam separados para OCR, tradução e ordem de leitura, mas compartilham uma mesma máscara e uma mesma repintura.

```text
TextLayer A ┐
            ├─ Grupo de mesclagem
TextLayer B ┘
              ├─ Máscara mesclada
              └─ Repintura mesclada
```

Esse fluxo é útil quando duas falas estão próximas ou quando as máscaras se encostam visualmente, mas os textos ainda precisam continuar independentes.

## Estrutura de projeto

Novos projetos usam uma estrutura própria do MangaTypesetter:

```text
MeuProjeto/
├─ MangaTypesetterProject.mtp
├─ Chapter.mtchapter
├─ original/
├─ export/
├─ assets/
├─ autosave/
├─ masks/
├─ inpainting/
└─ cache/
```

O arquivo `.mtp` guarda informações gerais do projeto, como metadados, template, idiomas, modo de leitura e referência para o capítulo.

O arquivo `.mtchapter` guarda páginas, camadas, vínculos entre texto/máscara/repintura, grupos de mesclagem, campos de OCR/tradução e a última página aberta.

Os arquivos usam extensões próprias do MangaTypesetter para facilitar a organização do projeto.

## Recursos implementados

### Projetos e páginas

- Criação de novo projeto.
- Abertura e salvamento de projeto.
- Recuperação básica por autosave.
- Importação de imagens.
- Organização de páginas com ordenação natural.
- Lista lateral de páginas com miniaturas.
- Suporte a capítulos com múltiplas páginas.

Formatos de imagem suportados no fluxo principal:

```text
png, jpg, jpeg, webp, bmp, tif, tiff
```

### Canvas e navegação

- Canvas visual para edição de páginas.
- Zoom.
- Pan.
- Ajuste à tela.
- Seleção de camadas no canvas.
- Movimento e redimensionamento básico de áreas de texto.
- Movimento de camada selecionada com as setas do teclado.

### Camadas

O editor trabalha com diferentes tipos de camada:

- imagem;
- texto;
- limpeza;
- máscara;
- inpainting/repintura.

O painel de camadas permite:

- selecionar camadas;
- alternar visibilidade;
- bloquear edição;
- organizar ordem/profundidade;
- remover camadas;
- trabalhar com relações entre texto, máscara e repintura.

### Texto e typesetting

Cada área de texto pode manter diferentes versões do conteúdo:

- texto original/OCR;
- texto traduzido;
- texto aplicado na página.

Recursos de estilo disponíveis:

- fonte;
- tamanho;
- cor;
- alinhamento;
- opacidade;
- margens;
- auto size;
- negrito;
- itálico;
- stroke/contorno;
- múltiplos strokes;
- rotação;
- posição;
- tamanho da caixa de texto;
- ordem de leitura.

Também há suporte a estilos padrão por template, permitindo que novas camadas de texto já nasçam com uma aparência configurada.

### Ferramentas de edição

Ferramentas disponíveis ou em estágio inicial:

- seleção;
- texto;
- limpeza retangular;
- pan;
- zoom;
- seleção retangular;
- seleção elíptica;
- laço;
- laço poligonal;
- varinha mágica;
- transformação básica.

A varinha mágica permite selecionar regiões conectadas por similaridade de cor, o que pode ajudar na seleção de balões, fundos planos e áreas brancas.

### Detecção, OCR, máscara e repintura

O MangaTypesetter possui integrações locais para auxiliar o fluxo de edição:

- detecção de balões e áreas de fala;
- OCR local;
- geração de máscara com OpenCV;
- inpainting/repintura local;
- criação automática do fluxo `TextLayer -> MaskLayer -> InpaintLayer` após detecção;
- regeneração de máscaras;
- mesclagem manual de máscaras entre textos;
- configuração inicial de mesclagem automática de máscaras.

As máscaras ficam ocultas por padrão, pois normalmente são usadas apenas como apoio para limpeza e repintura.

### Tradução e glossário

O app possui recursos voltados para revisão e tradução:

- janela de tradução;
- exportação e importação de texto em TXT/JSON;
- glossário próprio;
- importação/exportação de glossário;
- organização de ordem de leitura;
- campos separados para OCR, tradução e texto final aplicado.

Esses recursos ajudam a manter o texto bruto, o texto revisado e o texto final separados durante o processo de edição.

### Exportação

Recursos de exportação disponíveis:

- exportar página atual;
- exportar capítulo;
- renderizar imagem original, limpeza, repintura e texto final;
- ignorar máscaras auxiliares no resultado final.

## Atalhos principais

- `V`: ferramenta de seleção
- `T`: ferramenta de texto
- `C`: limpeza retangular
- `Espaço`: pan temporário
- `Ctrl+S`: salvar
- `Ctrl+0`: ajustar zoom
- `Ctrl+Scroll`: zoom
- `Delete`: remover camada selecionada
- `Ctrl+Z`: desfazer
- `Ctrl+Y` / `Ctrl+Shift+Z`: refazer
- Setas: mover camada de texto selecionada
- `Shift + Setas`: mover camada de texto com passo maior

## Estado atual

O MangaTypesetter já possui uma base funcional para trabalhar com projetos, páginas, camadas, texto, máscaras, OCR, detecção e repintura.

O fluxo principal de detecção, criação de texto, geração de máscara e inpainting já existe, mas ainda precisa ser validado em mais páginas reais e em capítulos maiores.

Algumas áreas ainda estão em consolidação:

- mesclagem automática de máscaras;
- edição direta de texto no canvas;
- ferramentas avançadas de transformação;
- exportação avançada;
- tradução em lote com contexto;
- desempenho em capítulos muito grandes ou webtoons longos;
- ferramentas manuais mais próximas de editores como Photoshop.

## Limitações conhecidas

- A mesclagem automática de máscaras ainda é experimental.
- Alguns fluxos de tradução e importação/exportação de texto ainda precisam de mais testes em projetos grandes.
- A edição direta de texto no canvas ainda não está finalizada.
- Ferramentas avançadas como transformação por perspectiva, distorção, carimbo, pincel de máscara e edição manual refinada ainda fazem parte dos planos futuros.
- O suporte a capítulos muito longos precisa de otimizações adicionais de carregamento, cache e visualização contínua.

## Ideias futuras

Recursos planejados ou desejados para versões futuras:

- visualização contínua do capítulo, com páginas uma abaixo da outra;
- renderização virtualizada para capítulos grandes e webtoons;
- edição direta do texto no canvas;
- normalização de OCR para corrigir palavras quebradas por hífen;
- criação de máscaras a partir de seleções manuais;
- editor de máscara com pincel e borracha;
- transformação avançada de texto e camadas;
- suporte melhor a SFX;
- exportação com presets de qualidade e nomenclatura;
- exportação para formatos de pacote de capítulo;
- revisão em lote de OCR e tradução;
- glossário mais avançado;
- memória de tradução;
- presets de estilo por personagem ou tipo de fala.

## Status do projeto

MangaTypesetter está em desenvolvimento ativo.

A documentação deste repositório descreve o conceito, os recursos e o estado atual do aplicativo. O código-fonte principal é privado.
