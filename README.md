# boletime-latex

![Capa do BoletIME](https://camat.ime.usp.br/images/boletime/newsletter/capa_fundo_branco.jpg)

Modelo em LaTeX para o BoletIME!

Até então o BoletIME vem sendo produzido no Canva. Isso não só dificulta a passagem dos textos para o site, como também cria uma forte dependência de quem manja da ferramenta. Como o LaTeX é uma ferramenta comum a todos no IME, cabe usá-lo.

## Código-fonte

_Última sincronização com o Overleaf: 03.01.2025_

O código-fonte se encontra neste repositório, mas pode ser que não esteja sempre sincronizado com o Overleaf. Se for usar o template, recomendo ter uma conta no Overleaf (logicamente) e fazer uma cópia do seguinte projeto:

https://www.overleaf.com/read/xcfynzcbncbc#1d4cea

## Como fazer?

Não colocarei detalhes do LaTeX aqui. A documentação é pública, basta ir atrás.

O essencial é o que segue.

### Configurando a edição

O arquivo "config_edicao.tex" deve ser atualizado com as informações básicas da edição:

```latex
% Número da edição
\def\edicao{11}

% Mês e ano da edição
\def\mes{maio}
\def\ano{2024}
```

### Configurando o sumário

O arquivo "sumario.tex" gera a seção central da primeira página, onde temos os textos, avisos etc. Ele deve ser editado conforme o resto do arquivo.

Para adicionar itens do sumário, basta usar o comando `\itemSumario`:

```latex
\itemSumario{Título}{Texto}{Nº da página}
```

Costumamos adicionar um quadradinho com alguma coisa dentro também. Temos um comando  `\quadradao`:

```latex
\quadradao{Tamanho da fonte}{Espaçamento}{Espaço entre as letras}
{Comprimento do quadrado}{Cor}{Tamanho da borda}{Texto}
```

Como as unidades do LaTeX são confusas, segue um exemplo:

```latex
\quadradao{\LARGE}{1.4}{50}{.9\textwidth}{vermelho_camat}{0.2cm}{
- É pavê ou pacumê?\\
- Sim.}
```

### Textos

Os textos podem ser adicionados em arquivos separados dentro do diretório "textos", e as imagens utilizadas podem estar dentro do diretório "textos/img".

O arquivo que junta todos os textos é o "textos.tex", basta usar o comando `\input`:

```latex
\input{textos/arquivo}
```

O BoletIME usualmente tem as páginas divididas em duas colunas. Isso é feito através do pacote `multicols`. Dentro do arquivo "texto.tex", o que quiser que esteja formatado em duas colunas precisa estar dentro do ambiente `multicols`:

```latex
\begin{multicols*}{2}
pipipi pópópó
\end{multicols*}
```

Se quiser ir para a outra coluna, basta utilizar a combinação de comandos:

```latex
\vfill\null\columnbreak
```

O `*` no nome do ambiente faz com que as colunas cubram toda a página, em vez de se quebrarem conforme o tamanho do texto. Caso queira a formatação dependente do tamanho do texto, basta tirar o `*`. Além disso, se estiver no ambiente `multicols*` e quiser colocar algo no final da página, basta usar o separador `\vfill`:

```latex
\begin{multicols*}{2}
Isso está no começo da página.
\vfill
Isso está no final da página.
\end{multicols*}
```

No caso de precisar utilizar somente 1 coluna em algum momento, não utilize `\begin{multicols*}{1}`, isso não faz sentido. Basta colocar o conteúdo fora do ambiente `multicols`.

Frequentemente também precisamos de separadores. Temos um comando para isso.

```latex
\barraVermelha
```

#### Textos enviados por leitores

```latex
\section*{Título do texto}
\autoria{por Autor}
\avisoTextoForms
```

O comando `\avisoTextoForms` adiciona o avisinho vermelho indicando que o texto não necessariamente corresponde com a opinião do editorial.

#### Seções especiais

Algumas sessões do texto, como a de poesias, recebem uma formatação diferente. Por exemplo:

```latex
\tituloCaixa{SEÇÃO DE POESIAS}

Conteúdo
```

Também pode ser útil centralizar o título da seção. Nesse caso, utilize o comando `\tituloCentralizado`:

```latex
\tituloCentralizado{Título centralizado}
```

#### Imagens no meio do texto

Como dito, coloque as imagens no diretório "textos/img". Para adicionar no texto, use o ambiente `figure` padrão, mas não utilize o comando `\caption`, pois ele tem sua própria formatação. Utilize o `\legendaFigura` no lugar.

```latex
\begin{figure}[H]
    \centering
    \includegraphics[width=0.5\linewidth]{textos/img/figura.jpg}
    \\
    \legendaFigura{1}{Legenda da figura.}
\end{figure}
```

O número `1` ali configura o tamanho do espaçamento entre linhas. Quando a legenda tiver mais de um parágrafo, é necessário utilizar o comando `\legendafiguraQuebraLinha`.

```latex
\begin{figure}[H]
    \centering
    \includegraphics[width=0.5\linewidth]{textos/img/figura.jpg}
    \legendaFigura{1.2}{
        Primeira linha da legenda.
        \legendaFiguraQuebraLinha
        Segunda linha da legenda.
    }
\end{figure}
```

#### Citações

Às vezes o pessoal usa citações longas e/ou que precisam estar em espaços separados. Para isso, utilize o ambiente `\displayquote`:

```latex
\begin{displayquote}
    75 foi um ano complicado.
\end{displayquote}
```

## Gerando os arquivos finais

### Versão digital (colorida)

Normalmente nós precisamos de duas versões do BoletIME: uma digital e uma para impressão. A versão digital é gerada através do próprio arquivo "main.tex", basta compilá-lo e baixar o PDF.

### Versão para impressão

A versão para impressão é diferente. Primeiro, compile o arquivo "versao_pb.tex", no qual as principais cores do documento (texto, página etc) serão substituídas por um tom de cinza. Baixe o arquivo e aplique algum processo de monocromatização. Sugiro utilizar o [online2pdf](https://online2pdf.com/pdf-change-color-to-black-and-white).

Em seguida, suba o arquivo monocromático com o nome de "boletime.pdf" para a raiz do diretório, e compile o documento "booklet.tex". Baixe o arquivo final. Este estará pronto para impressão no formato "booklet", com o **giro da página sendo feito pela borda maior**.
