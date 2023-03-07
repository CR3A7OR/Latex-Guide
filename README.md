
<div align="center" width="100%">
    <img src=".\img\title.png" width="75%" height="75%" alt="title">
    <h4>│ Guide for Latex  │</h4>
    &nbsp;
</div>

The following file shows a simplified guide through my insight of using Latex, including a latex template which I used for assignments during University. The following guide will show an overview of some simple setup, breadown, useful sources and troubleshooting of the following template. However, the abstracted components shown can be applied to any Latex file.


| Index  | Description |
|--------|---------|
| [Template](#templace) | Covering the available template in this git |
| [Figures / Tables](#figures) | Adding Figures and Tables to file |
| [Maths](#maths) | Adding math equations and symbols |
| [Code Snippets](#code) | Adding code snippters  |
| [References](#references) | Creating a bibliography  |
| [TroubleShooting](#troubleshoot) | Common problems and solutions  |

## **My Setup**
Whilst [Overleaf](https://www.overleaf.com/) is an excellent tool for Latex. The setup which I use for editiing and producing documents in Latex relies on the following elements: \
**IDE**: Atom <img src=".\img\atom.png" width="13px"> \
**Packages**:  

<img align="left" src=".\img\packages.png" width="296px" height="75%" alt="packages"> 

- Notes:
    - » **pdf-view** : For this to operate as expected, showing the compiled PDF side by side, change `Viewer` tab in Settings for **latextools** to the pdf-view 
    - » Does not include any grammar checks, quick online alternative: [**Scribens**](https://www.scribens.com/)


<br clear="left"/>

To compile the latex file you need to have selected `Template.tex` and then press `Ctrl + Alt + B`, this should generate a bunch of files including the PDF document which will be opened and split the IDE in two.

<div align="center">
    <img src=".\img\split.png" width="75%" alt="split">
</div>


# <a name="templace"></a>»│ Assignment Template

The template has been structured for easy use and modification with most adjustmenets being needed inside the main `Template.tex` file. The design of template is predominatly defined within the *MastersDoctoralThesis* file . The structure of the core files:
```
📂Latex Template
└📁img
└📁seperate 
    - CODESNIPPETS.txt
    - biblio.bib
    - Template.tex
    - MastersDoctoralThesis.cls
    - *.sty
```
 - `img` folder should contain all images 
 - `seperate` folder should each seperate section of your document
     - creating a new X.tex file can be added with `\input{seperate/X.tex}`
     - Hierarchy inside of files can be:
         ```
         \section 
            \subsection 
                \subsubsection 
                    \subparagraph
         ```
 - `CODESNIPPETS.txt` file with all code snippets to be displayed
 - `biblio.bib` file with all references to be cited
 - `Template.tex` main file handling libraries, initial setup
 - `MastersDoctoralThesis`
 - `*.sty`

Updating the margins of this document can be adjusted in the following section:
```tex
\geometry{
	paper=a4paper, % Change to letterpaper for US letter
	inner=2.5cm, % Inner margin
	outer=3.8cm, % Outer margin
	bindingoffset=.5cm, % Binding offset
	top=1.5cm, % Top margin
	bottom=1.5cm, % Bottom margin
	%showframe, % Uncomment to show how the type block is set on the page
}
```

# <a name="figures"></a> »│ Figures / Tables

 
Figure image directories have the absolute path defined in the line `\graphicspath{{./img/}}`. To add **figures** to a document you can use:

```tex
\begin{figure}[H]
    \centering
    \includegraphics[width=1\textwidth]{FILENAME}
    \caption{CAPTION}
    \label{fig:LABEL}
\end{figure}
```
Placing figures to be side by side adding the subfigure embeds creates these: 
```tex 
\begin{figure}[H]
\centering
    \begin{subfigure}{0.5\textwidth}

    \end{subfigure}
    \begin{subfigure}{0.4\textwidth}

    \end{subfigure}
\end{figure}
```
To add **tables** to a document you can use:
```tex
\begin{table}[htbp]
\centering
\begin{tabular}{||c | p{7cm} ||}
 \hline
  Table Name & Table Name \\ [0.5ex]
 \hline
  Content & Content \\
 \hline
  Content & Content \\ [1ex]
 \hline
\end{tabular}
\caption{Caption}
\label{table:1}
\end{table}
```

Tables and figures can be referenced throughout documents using :
> \textbf{Figure \ref{fig:LABEL}} \
> \textbf{Table \ref{table:LABEL}}

# <a name="maths"></a> »│ Adding Maths

A strong benefit of Latex is the ability to represent math equations within a PDF document \
Two ways of using the dollar symbols ($): \
1. 
<div align="center">

`$E=mc^{2}$` --> $E=mc^{2}$ 
&nbsp;
</div>
2.
<div align="center">

⬇️ `$$ E=mc^{2} $$`  ⬇️
</div>

 $$ E=mc^{2} $$

The capabilities of Latex maths is quite extensive in syntax. An intuitive guide for creating formulas can be found [**here**](https://latex.codecogs.com/eqneditor/editor.php) 

# <a name="code"></a> »│ Code Snippets & Languages

A rudamentary approach to listing code is using pseudo code which can be made with the `\algorithmic` and `\algorithm` library: 
```tex
\begin{algorithm}[H]
  \caption{Perceptron training pseudocode}\label{alg:Percept}
	\begin{algorithmic}
    \Procedure{PerceptronTrain}{$D, MaxIter$}
      \State $w_{i}=0$ for all $i=1,..,d$
      \State $b=0$
      \For{$iter=1...MaxIter$}
        \For{$all(classIdentfier,\overline{X},y) \in D$}
          \State $a= \overline{W^{T}}\overline{X} + b$
          \If{$y \cdot a \leq 0$}
            \State $w_{i} = w_{i} + y \cdot x_{i}$ for all $i = 1,..,d$
            \State $b = b + y$
          \EndIf
        \EndFor
      \EndFor
    \State \textbf{return} $b, w_{1},w_{2},...,w_{d}$
    \EndProcedure
  \end{algorithmic}
\end{algorithm}
```
⬇️

<img src=".\img\pseudoCode.png" width="50%" alt="split">

However to add the code snippet below into your PDF you can use the `\listing` first paste it into CODESNIPPETS.txt and record the lines it reaches across:
```py
1 @app.route('/')
2 def index():
3    date = getDate()
4    data = getArticles()
5    return render_template('index.html', date=date, data=data)
```
You can call these lines with the highlighted syntax into your .tex file using:
```tex
\begin{figure}[H]
  \lstinputlisting[language=Python, firstline=1, lastline=5]{CODESNIPPETS.txt}
  \caption{CAPTION}
  \label{Realisation:1}
\end{figure}
```
⬇️

<img src=".\img\python.png" width="75%" alt="split">

The listings library provides a coverage of many [languages](https://en.wikibooks.org/wiki/LaTeX/Source_Code_Listings#Supported_languages) for syntax highlighting but not all, two ways to extend this availability is to use a `.sty` file adding it to `\usepackage{listings, listings-rust}` or manually add the rules using `\lstdefinelanguage{JavaScript}{}`. 

# <a name="references"></a> »│ References 

Refernces in the template use biblatex backend and mean you can copy biblatex formatted references into the `biblio.bib` file and then use:
- `\cite{}` - Citing a source in passing
- `\parencite{}` - Citing quotes, produces same format as \cite but with ()

> Useful note to add url and date accessed to a reference inside biblatex ref formart:
> - url="URL" (containing the URL of where source was found)
> - addendum = "(Accessed: DD.MM.YYYY)" (when a source was accessed)

You can convert biblatex citations into other formats using this [Biblatex converter](https://bibtex.online/#)

---
## <a name="troubleshoot"></a> »│ TroubleShooting 

1. Bibliography reporting undefined references on compile
    - Open CMD and type `bibtex ./biblio.bib`
    
<div align="center">
--- [ 𝗖𝗥𝟯𝗔𝗧𝟬𝗥 ] // Designed By --- 
</div>
