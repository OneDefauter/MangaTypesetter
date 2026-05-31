# Exportação

A exportação gera imagens finais do projeto.

## Destino

Toda exportação salva automaticamente em:

```text
<projectDir>/export/
```

O app não pergunta mais onde salvar.

## Exportar Página

Exporta apenas a página atual.

Nome padrão:

```text
001.png
002.png
003.png
```

## Exportar Capítulo

Exporta todas as páginas válidas do projeto.

O processo roda em background.

Durante exportação:

* a UI continua responsiva;
* o progresso mostra página atual;
* o progresso mostra etapa atual;
* é possível cancelar.

## Configurações de Exportação

Em `Configurações > Exportar`:

* formato: PNG, JPG/JPEG ou WEBP;
* qualidade JPG/WebP;
* compressão PNG;
* sobrescrever existentes;
* abrir pasta ao concluir;
* exportar layers invisíveis;
* exportar máscaras;
* threads de exportação;
* escala;
* qualidade de texto.

## PNG

PNG é sem perdas.

Recomendado para:

* mangá preto e branco;
* line art;
* páginas com poucos tons.

Opções:

* compressão PNG `0..9`;
* otimização PNG;
* conversão para grayscale quando possível;
* remoção de alpha quando a saída é opaca.

## JPG

JPG usa perda de qualidade, mas gera arquivos menores.

Recomendado para:

* páginas coloridas;
* webtoon/manhua;
* distribuição web.

## WEBP

WEBP pode gerar boa qualidade com tamanho menor, mas depende do suporte do Qt/plugin no build.

## Logs de Exportação

O app registra:

* início/fim do job;
* configurações usadas;
* número real de threads;
* tempo por página;
* tempo por layer;
* tamanho final de arquivo;
* aviso de PNG quase sem compressão.

Use o analisador:

```powershell
python tools/analyze_continuous_trace.py .\logs\trace_arquivo.mtrace
```

