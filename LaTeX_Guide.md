# LaTeX_Guide

## Table des matières

1. [LaTeX_Guide](#latex_guide)
   1. [Table des matières](#table-des-matières)
   2. [Insérer des figures](#insérer-des-figures)
      1. [Insérer une image simple avec légende et label](#insérer-une-image-simple-avec-légende-et-label)
      2. [Insérer plusieurs images à l'aide de subfigure](#insérer-plusieurs-images-à-laide-de-subfigure)
      3. [Règles de positionnement des figures](#règles-de-positionnement-des-figures)
   3. [Insérer des tableaux](#insérer-des-tableaux)
   4. [Intégrer des équations](#intégrer-des-équations)
      1. [Créer des équations en ligne](#créer-des-équations-en-ligne)
      2. [Intégrer une équation à la liste des équations](#intégrer-une-équation-à-la-liste-des-équations)
   5. [Intégrer des codes](#intégrer-des-codes)
      1. [Intégrer un bout de code de quelques lignes](#intégrer-un-bout-de-code-de-quelques-lignes)
      2. [Intégrer un bout de code de quelques lignes mais en format court](#intégrer-un-bout-de-code-de-quelques-lignes-mais-en-format-court)
      3. [Intégrer un code d'une ligne dans un bloc de texte](#intégrer-un-code-dune-ligne-dans-un-bloc-de-texte)
      4. [Intégrer un code depuis un fichier, voire un fragment de ce fichier](#intégrer-un-code-depuis-un-fichier-voire-un-fragment-de-ce-fichier)
   6. [Début de document classique (alternative à la page de garde proposée)](#début-de-document-classique-alternative-à-la-page-de-garde-proposée)

## Insérer des figures

### Insérer une image simple avec légende et label

````
\begin{figure}[htbp]
    \centering
    \includegraphics[width=\textwidth]{example-image-a.png}
    \caption{Image A}
    \label{fig:example-image-a} % Bon réflexe de garder le même nom de fichier et de label
\end{figure}
````

### Insérer plusieurs images à l'aide de subfigure

````
\begin{figure}[H]
    \begin{subfigure}[t]{0.475\textwidth}
        \includegraphics[width=1\textwidth]{example-image-b}
        \caption{Image B}
        \label{subfig:example-image-b}
    \end{subfigure}%
    ATTENTION, le % est très important ici pour éviter les problèmes de vide
    \hfill    % Remplissage entre les images
    \begin{subfigure}[t]{0.475\textwidth}
        \includegraphics[width=1\textwidth]{example_image_c}
        \caption{Image C}
        \label{subfig:example-image-c}
    \end{subfigure}
    \caption{Exemple d'utilisation des sous-figures}
    \label{fig:test_subfigure}
\end{figure}
````

### Règles de positionnement des figures

- **h** : Place the float here, i.e., approximately at the same point it occurs in the source text (however, not exactly at the spot)
- **t** : Position at the top of the page.
- **b** : Position at the bottom of the page.
- **p** : Put on a special page for floats only.
- **!** : Override internal parameters LATEX uses for determining "good" float positions.
- **H** : Places the float at precisely the location in the LATEX code. Requires the float package (\usepackage{float}). This is somewhat equivalent to h!, though some errors may arise if you have too many consecutive floats with [H].

## Insérer des tableaux

- <https://www.tablesgenerator.com/> : Pour un tableau non évolutif et une interface sympathique.
- <https://www.latex-tables.com/> : Pour pouvoir les rééditer facilement.

## Intégrer des équations

### Créer des équations en ligne

- <https://latex.codecogs.com/eqneditor/editor.php> : Pour créer des équations en ligne.

### Intégrer une équation à la liste des équations

````
\noteworthy{equation}{légende} pour l'avoir dans la liste des équations
````

## Intégrer des codes

### Intégrer un bout de code de quelques lignes

````
\begin{listing}[htbp]
    \begin{minted}{c}
    #include <stdio.h>
    int main() {
    printf("Hello, World!"); /*printf() outputs the quoted string*/
    return 0;
    }
    \end{minted}
    \caption{Hello World in C}
    \label{listing:2}
\end{listing}
````

### Intégrer un bout de code de quelques lignes mais en format court

````
\mint{python}|print("hello")| % Équivalent de \minted mais plus court
````

### Intégrer un code d'une ligne dans un bloc de texte

````
\mintinline{python}|print("hello")|   % Quand t'as qu'une ligne de code
````

> Remarque : Le séparateur aurait pu être { } ou d'autres ponctuations

### Intégrer un code depuis un fichier, voire un fragment de ce fichier

````
\inputminted[firstline=2, lastline=12]{octave}{BitXorMatrix.m}
````

___

## Début de document classique (alternative à la page de garde proposée)

````
\title{Titre}
\author{Auteur}
\date{\today}
\maketitle
\begin{abstract}
    Blablabla
\end{abstract}
````
