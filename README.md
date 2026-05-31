# MangaTypesetter

MangaTypesetter é um editor desktop em desenvolvimento para tradução, limpeza, redesenho e typesetting de páginas de mangá, webtoon e manhua.

A proposta do aplicativo é reunir em um único fluxo as etapas mais comuns de preparação de capítulos: importar páginas, detectar balões ou áreas de fala, executar OCR, revisar/traduzir textos, gerar máscaras, limpar ou repintar regiões da imagem, aplicar o texto traduzido e exportar o resultado final.

> Status: em desenvolvimento ativo. A base do editor já existe, mas várias funções avançadas ainda estão em validação ou consolidação.

---

## Wiki

Para acessar a Wiki é [aqui](./doc/README.md)

## Objetivo

O MangaTypesetter foi pensado para facilitar o trabalho de edição de capítulos completos, evitando que cada página precise ser tratada como uma imagem isolada.

O aplicativo trabalha com um projeto de capítulo, mantendo imagens originais, páginas, camadas, textos, máscaras, repinturas, configurações de OCR/tradução e arquivos exportados organizados em uma estrutura própria.

Principais objetivos:

- importar e organizar páginas de mangá, webtoon e manhua;
- criar áreas de texto manualmente;
- detectar balões e áreas de fala automaticamente;
- executar OCR em páginas, áreas selecionadas ou camadas de texto;
- gerar máscaras para limpeza do texto original;
- usar inpainting/repintura para reconstruir regiões apagadas;
- aplicar texto traduzido com controle de estilo;
- revisar a ordem de leitura;
- exportar páginas ou capítulos finalizados.

---

## Fluxo principal

O fluxo esperado para uma página é:

1. Importar as páginas do capítulo.
2. Detectar balões automaticamente ou criar áreas de texto manualmente.
3. Criar uma camada de texto para cada fala ou área detectada.
4. Executar OCR quando necessário.
5. Revisar o texto original/OCR.
6. Traduzir ou importar a tradução.
7. Gerar máscara para a região do texto original.
8. Aplicar limpeza ou inpainting na área mascarada.
9. Ajustar fonte, tamanho, cor, contorno, alinhamento, posição, rotação e ordem de leitura.
10. Exportar a página ou o capítulo finalizado.

Relação básica entre camadas:

```text
TextLayer
├─ MaskLayer
└─ InpaintLayer
```

Também há suporte a grupos de mesclagem, onde duas ou mais camadas de texto continuam independentes para OCR, tradução e ordem de leitura, mas podem compartilhar máscara e repintura quando suas regiões se encostam visualmente.

```text
TextLayer A ┐
TextLayer B ┘
├─ Máscara mesclada
└─ Repintura mesclada
```

---

## Estrutura de projeto

Novos projetos usam uma estrutura própria:

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

O arquivo `.mtp` guarda informações gerais do projeto, como nome, obra, capítulo, idiomas, template, modo de leitura e caminho do capítulo.

O arquivo `.mtchapter` guarda páginas, camadas, vínculos entre texto/máscara/repintura, grupos de mesclagem, campos de OCR/tradução e a última página aberta.

---

## Recursos implementados

### Projetos e páginas

- Criação de novo projeto.
- Abertura e salvamento de projeto.
- Importação de imagens.
- Organização de páginas com ordenação natural.
- Lista lateral de páginas com miniaturas.
- Suporte a capítulos com múltiplas páginas.
- Autosave básico.
- Templates iniciais para diferentes fluxos de leitura.

Formatos de imagem usados no fluxo principal:

```text
png, jpg, jpeg, webp, bmp, tif, tiff
```

### Canvas e navegação

- Canvas visual para edição de página.
- Modo paginado.
- Modo contínuo para capítulos/webtoons.
- Zoom.
- Pan.
- Ajuste à tela.
- Visualização em tamanho real.
- Seleção de camadas no canvas.
- Movimento e redimensionamento básico de camadas de texto.
- Movimento da camada selecionada com as setas do teclado.
- Painéis flutuantes para controle e texto.

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
- organizar profundidade/ordem;
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
- alinhamento horizontal;
- alinhamento vertical;
- opacidade;
- margens;
- auto size;
- negrito;
- itálico;
- rotação;
- posição;
- tamanho da caixa de texto;
- ordem de leitura;
- stroke/contorno;
- múltiplos strokes;
- gradiente em stroke.

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

A varinha mágica permite selecionar regiões conectadas por similaridade de cor, ajudando em balões brancos, fundos planos e regiões de limpeza.

### Detecção, OCR, máscara e repintura

O MangaTypesetter possui integração com serviços locais em Python/FastAPI para auxiliar o fluxo de edição:

- detecção de balões e áreas de fala;
- OCR local;
- geração de máscara com OpenCV;
- inpainting/repintura local;
- criação automática do fluxo `TextLayer -> MaskLayer -> InpaintLayer` após detecção;
- regeneração de máscaras;
- mesclagem manual de máscaras entre textos;
- configuração inicial de mesclagem automática de máscaras;
- suporte a regiões que cruzam páginas no modo contínuo.

Serviços locais incluídos no projeto:

```text
resources/Python/ComicSpeechBubbleDetector  -> /detect
resources/Python/PaddleOCR                  -> /ocr
resources/Python/MangaOCR                   -> /ocr
resources/Python/OpenCV                     -> /mask
resources/Python/IOPaint                    -> /inpaint
```

As máscaras ficam ocultas por padrão, pois normalmente são usadas apenas como apoio para limpeza e repintura.

### Tradução, glossário e APIs

O app possui recursos voltados para revisão e tradução:

- janela de tradução;
- campos separados para OCR, tradução e texto aplicado;
- organização de ordem de leitura;
- exportação/importação de textos;
- glossário próprio;
- importação/exportação de glossário;
- presets de provedores de API;
- configuração genérica de provedores sem recompilar o aplicativo.

Provedores previstos/configuráveis incluem:

- OpenAI/ChatGPT;
- Gemini;
- Google Translate;
- DeepL;
- LM Studio local;
- MangaOCR;
- PaddleOCR;
- IOPaint;
- OpenCV Mask;
- Comic Speech Bubble Detector;
- ComfyUI.

### Configurações

A janela de configurações possui categorias para organizar o comportamento do aplicativo:

- Geral;
- API;
- Template;
- Atalhos;
- Exportar;
- Máscara e Repintura;
- OCR;
- Detecção;
- Extensões;
- Sobre.

Também há configuração de:

- atalhos;
- provedores de API;
- templates;
- estilos de texto;
- exportação;
- máscara e inpainting;
- extensões Python;
- painéis flutuantes.

### Exportação

Recursos de exportação disponíveis:

- exportar página atual;
- exportar capítulo;
- renderizar imagem original, limpeza, repintura e texto final;
- ignorar máscaras auxiliares no resultado final;
- exportação assíncrona com progresso.

---

## Atalhos principais

| Atalho | Ação |
|---|---|
| `V` | Ferramenta de seleção |
| `T` | Ferramenta de texto |
| `C` | Limpeza retangular |
| `Espaço` | Pan temporário |
| `Ctrl+S` | Salvar projeto |
| `Ctrl+0` | Ajustar à tela |
| `Ctrl+1` | Tamanho real |
| `Ctrl+Scroll` | Zoom |
| `Delete` | Remover camada selecionada |
| `Ctrl+Z` | Desfazer |
| `Ctrl+Y` / `Ctrl+Shift+Z` | Refazer |
| `Setas` | Mover camada selecionada |
| `Shift + Setas` | Mover camada com passo maior |

---

## Estado atual

O MangaTypesetter já possui uma base funcional para:

- criar e abrir projetos;
- importar páginas;
- editar páginas em canvas;
- trabalhar com camadas;
- criar e editar textos;
- aplicar estilos de typesetting;
- usar ferramentas básicas de seleção;
- gerar máscaras;
- integrar OCR, detecção e inpainting local;
- exportar página ou capítulo;
- configurar APIs, templates, atalhos e extensões.

O app já passou da fase de protótipo conceitual. Ele ainda não está, porém, no nível de um editor finalizado como ImageTrans/Photoshop.

Áreas que ainda precisam de validação ou evolução:

- estabilidade do fluxo completo em capítulos grandes;
- detecção automática em diferentes tipos de mangá, manhua e webtoon;
- qualidade das máscaras em cenários difíceis;
- inpainting em textos sobre arte complexa;
- edição direta de texto no canvas;
- ferramentas manuais mais próximas de editores como Photoshop;
- transformação avançada/perspectiva;
- pincel e borracha para máscara;
- tradução em lote com contexto;
- revisão em lote;
- exportação avançada;
- desempenho em webtoons muito longos.

---

## Limitações conhecidas

- A mesclagem automática de máscaras ainda é experimental.
- A qualidade da detecção depende muito do tipo de página e do modelo usado.
- OCR e tradução ainda precisam de revisão humana.
- A edição direta de texto no canvas ainda não está finalizada.
- Ferramentas como carimbo, pincel de máscara, transformação por perspectiva e distorção ainda fazem parte dos planos futuros.
- O suporte a capítulos muito longos precisa de otimizações adicionais de carregamento, cache e renderização virtualizada.
- Algumas integrações externas exigem configuração local, modelos baixados ou chaves de API.

---

## Roadmap sugerido

### Curto prazo

- Consolidar o fluxo manual: criar texto, limpar, aplicar estilo e exportar.
- Melhorar estabilidade de salvamento/carregamento.
- Refinar seleção, varinha mágica e limpeza retangular.
- Melhorar painel de propriedades e edição de texto.
- Validar exportação de capítulos completos.

### Médio prazo

- Melhorar OCR por camada, página e capítulo.
- Refinar detecção automática de balões.
- Melhorar geração e edição de máscaras.
- Adicionar pincel/borracha de máscara.
- Melhorar integração com IOPaint.
- Aprimorar modo contínuo para webtoons.
- Melhorar tradução em lote e revisão com glossário.

### Longo prazo

- Suporte melhor a SFX.
- Transformação avançada de texto e camadas.
- Presets por personagem ou tipo de fala.
- Memória de tradução.
- Revisão em lote com status por página/balão.
- Exportação para pacotes de capítulo.
- Exportação avançada com presets de qualidade.
- Renderização virtualizada para capítulos muito grandes.
- Sistema de plugins/extensões mais completo.

---

## Stack

O projeto usa C++ com Qt para a aplicação desktop principal.

Serviços auxiliares de IA/OCR/processamento podem ser executados localmente com Python/FastAPI, mantendo o app principal como editor desktop nativo.

Estrutura geral:

```text
C++ / Qt
├─ Interface desktop
├─ Canvas
├─ Sistema de projeto
├─ Sistema de camadas
├─ Typesetting
├─ Exportação
└─ Integração com serviços locais

Python / FastAPI
├─ Detecção de balões
├─ OCR
├─ Geração de máscara
└─ Inpainting
```

---

## Status do projeto

MangaTypesetter está em desenvolvimento ativo.

A documentação descreve o conceito, os recursos implementados e o estado atual do aplicativo. Alguns recursos citados ainda são experimentais e podem mudar conforme o fluxo de edição for testado em capítulos reais.
