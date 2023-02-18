# Introduction to LaTeX
- [LaTex basics](README.md#latex-basics)
- [Math](README.md#math)
- [Figure](README.md#figure)
- [Table & List](README.md#table--list)
- [Appendix & Bibliography](README.md#appendix--bibliography)
- [Presentation](README.md#presentation)
- [Poster](README.md#poster)
- [LaTeX packages](README.md#latex-packages)
- [Examples](README.md#examples)
- [References](README.md#references)

## LaTeX basics
- LaTeX commands: `\command{option}`
- `\documentclass{}`: layout of the document
  - article, book, beamer
- `\begin{}`, `\end{}`: define an environment
  ```latex
  \begin{document}
    \begin{environment1}
      \begin{environment2}
    \end{environment1}
      \end{environment2}
  \end{document}
  ```
- `\title{}`
- `\date{}`
  - `\today`
- `\author{}`
- `\newpage`
- `\pagenumbering{}`
  - gobble, arabic, roman
- Texts
  - `text{}`: normal text
  - `textbf{}`: bold
- Table of contents
  - `\tableofcontents`
    - In preamble: `\setcounter{tocdepth}{n}`, where n = 1, 2, 3(default), 4, 5
    - Specify individually before each section: `\addtocontents{toc}{\setcounter{tocdepth}{3}}`
  - `\listoffigures`, `\listoftables`
- Sections: `\section{}`, `\subsection{}`, `\subsubsection{}`
- Paragraphs: `\paragraph{}`, `\subparagraph{}`

## Math
- Math environments: `$INLINE_FORMULA$`, `\(INLINE_FORMULA\)`, `equation`, `align`
  - use asterisk (e.g. `equation*`, `align*`) to turn-off auto numbering
  - math symbols
    - https://latex-tutorial.com/symbols/math-symbols/
    - most math symbols have to be used in the math environments
  - `\left`, `\right`: scale up the bracket symbol after it
  - Partitioned statements (with `amsmath` package):
    ```latex
    \[
    LHS =
      \begin{cases}
        RHS1, & \text{CONDITION1}\\
        RHS2, & \text{CONDITION2}
      \end{cases}
    \]
    ```

## Figure
- Figure environments
  - `\begin{figure}[placement specifier]`
    - h (here, if possible), t (top), b (bottom), p (page of floats), ! (override)
    - H (here, definitely) if `\usepackage{float}`
  - `\begin{subfigure}[pos][height][inner-pos]{width}`
    - pos: c (center, default), t (top), b (bottom)
    - height: strech the height of the subfigure (e.g. 10pt, 1cm)
    - inner-pos: t (top), c (center), b (bottom), s (stretch)
    - width: width of the subfigure
  - `\includegraphics[width=SIZE\textwidth]{FIGURE_PATH}`
    - SIZE: 0~1 (use 0.1 less than you expect)
  - `\caption{}`
  - `\label{MARKER}`: this MARKER can be used for later referencing
  - `\centering`
  - `\hfill`: make one figure left-align and the other right-align, then fill spaces to produce a rubber length (same as `\hspace\fill`)
  - `\hspace{L cm}`: L can be a positive or negative value.
  - `\ContinuedFloat`: preserve the numbering from the previous subfigures
 
 ## Table & List
- Table environment
  - `begin{table}`
  - `begin{tabular}{| l | c | r |}`
    - `l`: left-alignment, `c`: center-alignment, `r`: right-alignment, `S`: aligned decimal point (if `\usepackage{siunitx}`)
    - `|`: vertical line, `\hline`: horizontal line
    - in each row: `column1 & column2 & column3 \\`
    - for `\usepackage{multirow}`
      - multiple rows: `\multirow{NROWS}{WIDTH}{CONTENT}`
      - multiple columns: `\multicolumn{NCOLUMNS}{ALIGNMENT}{CONTENT}`
    - for long table, `\usepackage{longtable}`
      - `\begin{longtable}[placement specifier]{ALIGNMENT}`
      - Put the header between `\endfirsthead` and `\endhead` so that it will be shown on every page.
    - `usepackage{rotating}` to rotate the table
      - `\begin{sidewaystable}`
- List environment
  - `\begin{itemize}`, `\begin{enumerate}`
    - `\item ITEM 1`
    - `\item ITEM 2`
    - `\item ITEM n`
  - To change the bullet point symbol
    - `\item[?]`
    - `usepackage{enumitem}`, `usepackage{pifont}`
 
 ## Appendix & Bibliography
- Appendix environment
  - `\begin{appendix}`
- Referencing
  - `\label{KEY}`
  - `\ref{KEY}`, `\subref{KEY}`, `\pageref{KEY}`
  - `\footnote{\label{FOOTNOTE_LABEL} CONTENT}`, this footnote can be referred by using `\ref{FOOTNOTE_LABEL}`
  - `usepackage{hyperref}`
    - `\hyperref[KEY]{TEXT}` & `\hypertarget{KEY}{TEXT}`
    - `\url{URL}`, `\href{URL}{TEXT}`, `href{mailto:EMAIL}{TEXT}`, `\href{run:PATH/FILE}{TEXT}`
    - `\hypersetup{OPTION1=VALUE1,OPTION2=VALUE2,...}` (more information can be found in [LaTeX/Hyperlinks](https://en.wikibooks.org/wiki/LaTeX/Hyperlinks))
  - `usepackage{varioref}`
    - `\vref{KEY}`
  - `usepackage{cleveref}`
    - `\cref{KEY}`, `\Cref{KEY}`
- Bibliography
  - BibTeX
    ```latex
    \bibliographystyle{unsrt} % abbrv, alpha, acm, apalike, ieeetr, plain, unsrt
    \bibliography{bib_file1.bib, bib_file2.bib, ...}
    ```
    - `\cite{ReferenceKey}`, `\nocite{ReferenceKey}`
  - biblatex
    - in the preamble
      ```latex
      \usepackage[backend=bibtex, % biber, bibtex
      style=numeric, % numeric, alphabetic, authoryear, authortitle, verbose, reading, draft
      sorting=nyt % nty, nyt, nyvt, anyt, anyvt, ydnt, none
      ]{biblatex} 
      \addbibresource{bib_file1.bib}
      \addbibresource{bib_file2.bib}
      ```
    - in text
      - `\autocite[PAGE_NUM]{ReferenceKey}`, `\textcite[PAGE_NUM]{ReferenceKey}`
    - print the bibliography
      - `\printbibliography`
  - For more informations, please refer to these webpages
    -  https://www.overleaf.com/learn/latex/Bibliography_management_in_LaTeX
    -  https://www.overleaf.com/learn/latex/Bibtex_bibliography_styles
    -  https://www.overleaf.com/learn/latex/Bibliography_management_with_biblatex
    -  https://www.overleaf.com/learn/latex/Biblatex_bibliography_styles
  - Exporting references from reference managers
    - [Mendeley](https://www.mendeley.com/guides/mendeley-reference-manager/08.-exporting-references)
    - [Zotero](https://www.zotero.org/support/kb/exporting)
      - You may have to modify the title field manually with [rich text formatting](https://www.zotero.org/support/kb/rich_text_bibliography).

## Presentation
- LaTeX presentation environment
  - `begin{beamer}`
- Themes
  - `\usetheme{default}`
    - Boadilla, Madrid, Montpellier, Warsaw, ,Copenhagen, Goettingen, Hannover, Berkeley
- Title page
  - `\title{}`, `\subtitle{}`, `\author{}`, `\date{}`, 
  - `\titlegraphic{}`
  - `\titlepage`
- Logo
  - `\logo{}`
- Section
  - `\section{}`
- Frame
  - `\begin{frame}[label={LABEL}]{TITLE}{Subtitle}`
- Hyperlink
  - `\hyperlink{LABEL}{\beamerbutton{TEXT}}`

## Poster
- TikZ poster
  - `\documentclass[FONT_SIZE, PAPER_SIZE, ORIENT]{tikzposter}`
    - FONT_SIZE: 12pt, 14pt, 25pt, ...
    - PAPER_SIZE: a0paper, a1paper, a2paper, a3paper, a4paper
    - ORIENT: landscape, portrait
  - `\usetheme{}`
    - Default, Rays, Basic, Simple, Envelope, Wave, Board, Autumn, Desert
  - Title
    - `\maketitle`
  - Block
    ```latex
    \block{TITLE}
    {
      TEXT
    }
    ```
  - Columns
    ```latex
    \begin{columns}
      \column{WIDTH}
      \block{TITLE}{}
      \column{WIDTH}
      \block{TITLE}{}
    \end{columns}
    ```
- Beamer poster
  - `\documentclass{beamer}` + `\usepackage[orientation=portrait,size=a0,scale=1.4]{beamerposter}`
    - `orientation`: landscape, portrait
    - `size`: a0, a1, a2, a3, a4
    - `scale`
  - Themes
    - `\usetheme{}`
      - AnnArbor, Antibes, Bergen, Berkeley, Berlin, Boadilla, boxes, CambridgeUS, Copenhagen, Darmstadt, default, Dresden, Frankfurt, Goettingen, Hannover, Ilmenau, JuanLesPins, Luebeck, Madrid, Malmoe, Marburg, Montpellier, PaloAlto, Pittsburgh, Rochester, Singapore, Szeged, Warsaw
    - `\usecolortheme{}`
      - albatross, beaver, beetle, crane, default, dolphin, dove, fly, lily, orchid, rose, seagull, seahorse, sidebartab, structure, whale, wolverine
    - https://deic.uab.cat/~iblanes/beamer_gallery/index.html
  - Block
    ```latex
    \begin{frame}{}
      \begin{block}{TITLE}
        TEXT
      \end{block}
    \end{frame}
    ```
  - Columns
    ```latex
    \begin{frame}{}
    \begin{columns}[t]
      \begin{column}{WIDTH}
        \begin{block}{TITLE}
        \end{block}
      \end{column}
      \begin{column}{WIDTH}
        \begin{block}{TITLE}
        \end{block}
      \end{column}
    \end{columns}
    \end{frame}
    ```

## Journals
- [REVTeX](https://journals.aps.org/revtex)
  - Package: https://www.ctan.org/pkg/revtex
  - Usage: `\documentclass[OPTIONS]{revtex4-2}`
  - Documentation:
    - [PDF][APS Author Guide for REVTEX 4.2](https://ctan.math.illinois.edu/macros/latex/contrib/revtex/auguide/auguide4-2.pdf)
    - [PDF][Author's Guide to AIP Substyles for REVTEX 4.2](https://mirror.las.iastate.edu/tex-archive/macros/latex/contrib/revtex/aip/aipguide4-2.pdf)
    - [PDF][REVTEX 4.2 Command and Options Summary](https://ctan.math.illinois.edu/macros/latex/contrib/revtex/auguide/summary4-2.pdf)

## LaTeX packages
- LaTeX packages: `\usepackage{PACKAGENAME}`
  - all packages must be imported at the beginning
  - `geometry`: for page formatting, please refer to [geometry](https://ctan.org/pkg/geometry) document for more details.
  - `setspace`: change the spacing for table of contents by using `\singlespacing`, `\doublespacing`
  - `amsmath`:
    - equation numbering can be removed when using `begin{equation*} x=y end{equation*}` or `\nonumber` at the end of the equation
    - adding text in the equation with `\text{TEXT}`, `\mbox{TEXT}`
  - `graphicx`: for `figure` environment
  - `subcaption`: for `subfigure` environment
  - `booktabs`: for `tabular` environment, `\hline` can be replaced by `\toprule`, `\midrule` and `\bottomrule`
  - `tikz`: for drawing, please visit [TIKZ Blog](https://latexdraw.com/) for more examples
  - `circuitikz`: for drawing circuit diagram
  - `siunitx`: for aligning the decimal point
    - `\sisetup{round-mode= places, round-precision= 3}` (round-mode: places, figures)
  - `multirow`: for multiple rows in one cell
  - `longtable`: for long table
  - `rotating`: rotate the table
  - `pgfplotstable`: for autogenerated .csv tables
  - `pgfplots`: (part of `tikz`) for autogenerated plots
  - `listings`: for source code listings, another alternative is [minted](https://github.com/gpoore/minted)
  - `hyperref`: for hyperlinks
  - `varioref`: for cross-referencing on a different page
  - `cleveref`: for cross-referencing with automatic formatting
  - `enumitem`: for changing the bullet point symbol
  - `pifont`: for more bullet point styles, more symbols can be found in the [manual](https://ctan.org/pkg/pifont)
  - `blindtext`: generate dummy text
  - `beamer` & `beamerposter`: for presentations & posters

## Examples
- first_latex ([tex](/examples/1-first_latex.tex), [pdf](/examples/1-first_latex.pdf))
- paragraph_section ([tex](/examples/2-paragraph_section.tex), [pdf](/examples/2-paragraph_section.pdf))
- packages ([tex](/examples/3-packages.tex), [pdf](/examples/3-packages.pdf))
- math ([tex](/examples/4-math.tex), [pdf](/examples/4-math.pdf))
- figures ([tex](/examples/5-figures.tex), [pdf](/examples/5-figures.pdf))
- table_of_contents ([tex](/examples/6-table_of_contents.tex), [pdf](/examples/6-table_of_contents.pdf))
- bibliography ([tex](/examples/7-bibliography.tex), [pdf](/examples/7-bibliography.pdf))
- csv_tables/plots ([tex](/examples/8-csv_tables.tex), [pdf](/examples/8-csv_tables.pdf))
- presentation ([tex](/examples/9-presentation.tex), [pdf](/examples/9-presentation.pdf))
- poster ([tex-tikz](/examples/10a-tikzposter.tex), [pdf-tikz](/examples/10a-tikzposter.pdf); [tex-beamer](/examples/10b-beamerposter.tex), [pdf-beamer](/examples/10b-beamerposter.pdf))
- revtex ([tex](/examples/11-revtex_template.tex), [pdf](/examples/11-revtex_template.pdf))

## References
- https://latex-tutorial.com/tutorials/
- https://latex-beamer.com/
- https://vknight.org/tex/
- https://www.overleaf.com/learn/latex/Free_online_introduction_to_LaTeX_(part_1)
- https://www.overleaf.com/learn/latex/Posters
- https://en.wikibooks.org/wiki/LaTeX
- https://ctan.org/
- [PDF][LaTeX: A Document Preparation System by Leslie Lamport](http://users.softlab.ntua.gr/~sivann/books/LaTeX%20-%20User%27s%20Guide%20and%20Reference%20Manual-lamport94.pdf)
