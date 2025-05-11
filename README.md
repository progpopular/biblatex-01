# {La}TeXnicamente: Referências Bibliográficas em ABNT com LaTeX

[Programação Popular](https://www.youtube.com/@programacaopopular/)

- **Documentações**
  - [`biblatex-abnt` (CTAN)](https://ctan.org/pkg/biblatex-abnt)
  - [`hyperref` (CTAN)](https://ctan.org/pkg/hyperref)
- **Ferramentas usadas**:
  - [doi2bib](https://www.doi2bib.org/)
  - [Extensão BibItNow!](https://addons.mozilla.org/pt-BR/firefox/addon/bibitnow/)
  - [ISBN to BibTeX](https://www.bibtex.com/c/isbn-to-bibtex-converter/)
- **Referências citadas**:
[Cherkasov _et al._ (2014)](https://doi.org/10.1021/jm4004285),
[Cramer _et al._ (1988)](https://doi.org/10.1021/ja00226a005),
[Shi _et al._ (2015)](https://doi.org/10.1016/bs.mie.2015.02.001) e
[Roy _et al._ (2015)](https://www.amazon.com/Understanding-Applications-Pharmaceutical-Sciences-Assessment/dp/0128015055).

## Instruções para Compilar

Para compilar (gerar o PDF) este exemplo, você precisará de uma distribuição LaTeX, como [MikTeX](https://miktex.org) no Windows, [TeX live](https://www.tug.org/texlive) no Linux ou [Overleaf](https://www.overleaf.com) para trabalhar online.

Utilizamos o compilador [XeLaTeX](https://pt.overleaf.com/learn/latex/XeLaTeX) (incluído na maioria das distribuições LaTeX), o pacote [BibLaTeX](https://pt.overleaf.com/learn/latex/Bibliography_management_with_biblatex) e o estilo [`biblatex-abnt`](https://ctan.org/pkg/biblatex-abnt) para bibliografias.

Este código é potencialmente compatível com outros compiladores (como LuaLaTeX ou pdfLaTeX), mas não foi testado. O estilo `biblatex-abnt` é específico para BibLaTeX, mas usuários de BibTeX podem utilizar o [`abntex2cite`](https://tug.ctan.org/macros/latex/contrib/abntex2/doc/abntex2cite.pdf), embora não haja garantias de que ele esteja atualizado conforme as últimas normas ABNT.

### VSCode

Este repositório tem algumas configurações para [VSCode](https://code.visualstudio.com/) (editor utilizado no vídeo). Ao abrir o repositório no editor, serão sugeridas algumas extensões, das quais principalmente a [LaTeX Workshop](https://github.com/James-Yu/LaTeX-Workshop) é recomendada. A suite de compilação está pré-configurada.

### Compilação automática com `latexmk`

Caso você prefira não ter que se preocupar com quantas vezes cada compilador deve ser executado, utilize o [latexmk](https://ctan.org/pkg/latexmk). Ele está disponível na maioria das distribuições.

Para compilar com XeLaTeX, supondo que está no mesmo diretório de `main.tex`, utilize:

```bash
latexmk -xelatex main.tex
```

Para compilar com pdfLaTeX, utilize:

```bash
latexmk -pdf main.tex
```

Isso gerará o arquivo `main.pdf`.

Para limpar os arquivos auxiliares, utilize:

```bash
latexmk -C main
```

### Compilação manual

Para compilar manualmente, devemos seguir a seguinte sequência de compilação:

1. XeLaTeX
2. Biber
3. XeLaTeX
4. XeLaTeX

Assim, a sequência completa fica:

```bash
xelatex main
biber main
xelatex main
xelatex main
```

Nas compilações subsequentes, quando não houver alterações nos arquivos `*.bib`, não é necessário compilar com `biber`, situação em que a sequência de compilações pode ser:

```bash
xelatex main
xelatex main # caso necessário
```

Para compilar com pdfLaTeX, a sequência completa seria:
```bash
pdflatex main
biber main
pdflatex main
pdflatex main
```

Para saber com certeza quando compilar novamente ou não, observe as mensagens na saída do comando. Por exemplo, na primeira execução de `xelatex`:

```bash
$ xelatex main

[...]
LaTeX Warning: There were undefined references.


Package rerunfilecheck Warning: File `main.out' has changed.
(rerunfilecheck)                Rerun to get outlines right
(rerunfilecheck)                or use package `bookmark'.


Package biblatex Warning: Please (re)run Biber on the file:
(biblatex)                main
(biblatex)                and rerun LaTeX afterwards.

 )
Output written on main.pdf (5 pages).
Transcript written on main.log.
```

O aviso `Package biblatex Warning: Please (re)run Biber on the file main and rerun LaTeX afterwards.` (_Aviso do pacote biblatex: Por favor (re)execute Biber no arquivo main e reexecute o LaTeX após._) indica que devemos compilar com `biber`. Se fazemos isso, recebemos:


```bash
$ biber main

$ xelatex main

[...]
Package biblatex Warning: Please rerun LaTeX.
(biblatex)                Page breaks have changed.

 )
(see the transcript file for additional information)
Output written on main.pdf (3 pages).
Transcript written on main.log.
```

`Package biblatex Warning: Please rerun LaTeX. Page breaks have changed.` nos indica para compilar novamente.
Executando outra vez:

```bash
$ xelatex main

[...]
[5] (main.aux) )

Output written on main.pdf (5 pages).
Transcript written on main.log.
```

Sem avisos desta vez, portanto a compilação está completa.
