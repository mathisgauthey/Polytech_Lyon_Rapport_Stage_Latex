# Polytech Lyon : Template de rapport de stage

## Table des matières

1. [Polytech Lyon : Template de rapport de stage](#polytech-lyon--template-de-rapport-de-stage)
   1. [Table des matières](#table-des-matières)
   2. [Comment utiliser ce template ?](#comment-utiliser-ce-template-)
   3. [Configurations logiciel](#configurations-logiciel)
      1. [Configuration TexStudio](#configuration-texstudio)
      2. [Configuration VS Code](#configuration-vs-code)
         1. [Utiliser mon fichier settings](#utiliser-mon-fichier-settings)
         2. [Réaliser soi-même le paramétrage de l'extension Latex Wrokshop](#réaliser-soi-même-le-paramétrage-de-lextension-latex-wrokshop)
      3. [Configuration Sublime Text 3](#configuration-sublime-text-3)
   4. [Apprendre à utiliser LaTeX](#apprendre-à-utiliser-latex)
   5. [Licence du code](#licence-du-code)
   6. [Donations](#donations)
      1. [Pourquoi donner ?](#pourquoi-donner-)
      2. [Où effectuer un don ?](#où-effectuer-un-don-)

## Comment utiliser ce template ?

Template de rapport de stage (ou autre) en LaTeX utilisable à Polytech Lyon ou dans n'importe quelle école du réseau Polytech sous réserve de changer les images.
Nom du PDF final demandé à Polytech Lyon en date de la promotion 2021-2022 :

__AAAA_MM_5A_SPECIALITE_NOM_PRENOM__

Comment l'utiliser ?
Télécharger l'archive ou cloner le repo :
![image](https://user-images.githubusercontent.com/46576952/156882294-df1c6cbe-b5b8-4b1f-958f-65d4c2228846.png)

Puis l'importer et l'utiliser sur votre éditeur LateX (du plus user friendly au plus ~~horrible~~ complexe à mettre en place) :

- Overleaf
- Texstudio
- VS Code
- Sublime-Text-3

<ins>Attention :</ins> pour écrire en LaTeX en local sur votre PC, il vous faut une distribution LaTeX. *Je recommande ici d'installer **TexLive**.* En effet, les logiciels Texstudio, VS Code et Sublime-Text-3 sont des éditeurs de texte, mais votre PC a besoin d'un compilateur LaTeX pour fonctionner.

> NB : Une version exploitable a également été upload sur Overleaf : <https://fr.overleaf.com/latex/templates/polytech-lyon-rapport-stage-latex/xbjcfqjgfznt> \
Elle n'est pas maintenue à jour contrairement à ce repo, mais il devrait déjà y avoir de quoi faire.

## Configurations logiciel
### Configuration TexStudio

- Dans __Compilation__, choisir le paramètre de compilation PDFLaTeX : ``pdflatex.exe -synctex=1 -interaction=nonstopmode -shell-escape %.tex``
- Dans __Production__, choisir Biber en tant que moteur de bibliographie par défaut.
- Bien penser à appuyer sur F9 pour mettre à jour le glossaire quand il est modifié avant de compiler.
- Penser également à créer un user command "Make Nomenclature" : ``makeindex -s nomencl.ist -t %.nlg -o %.nls %.nlo`` (<https://www.youtube.com/watch?v=kW97Yv0-QC4>)
- Compiler avec F5 pour compiler et visualiser. La compilation peut se lancer plusieurs fois pour prendre en compte la bibliographie, bien attendre qu'il soit indiqué : ``system returned with code 1 Processus terminé normalement``. Autrement, vérifier les logs et corriger les erreurs.

### Configuration VS Code

#### Utiliser mon fichier settings

Aller dans `C:\Users\*USER_NAME*\AppData\Roaming\Code\User` et coller le fichier [settings.json](settings.json). That's it, Latex Workshop est paramétré correctement.

#### Réaliser soi-même le paramétrage de l'extension Latex Wrokshop

- Installer l'extension __Latex Workshop__ (<https://marketplace.visualstudio.com/items?itemName=James-Yu.latex-workshop>)
- Trouvez le paramètre "latex-workshop.latex.tools" dans les paramètres de l'extension.
- Ajoutez les latextools suivant :

```
        {
            "name": "pdflatex",
            "command": "pdflatex",
            "args": [
                "-synctex=1",
                "-interaction=nonstopmode",
                "-shell-escape",
                "-file-line-error",
                "%DOC%"
            ],
            "env": {}
        },
        {
            "name": "biber",
            "command": "biber",
            "args": [
                "%DOCFILE%"
            ],
            "env": {}
        },
        {
            "name": "index",
            "command": "makeindex",
            "args": [
                "-s",
                "nomencl.ist",
                "-t",
                "%DOCFILE%.nlg",
                "-o",
                "%DOCFILE%.nls",
                "%DOCFILE%.nlo",
            ],
            "env": {}
        },
        {
            "name": "glossary",
            "command": "makeglossaries",
            "args": [
                "%DOCFILE%"
            ],
            "env": {}
        },
```

- Compilez à l'aide du panneau latéral, ne pas hésiter à le refaire plusieurs fois pour vérifier que tout fonctionne, Latex est capricieux parfois. Le raccourcis pour build est ``ctrl+alt+b``.
- Trouvez le paramètre "latex-workshop.latex.recipes" dans les paramètres de l'extension.
- Ajoutez la recette suivante en première position :

```
        {
            "name": "master compiler",
            "tools": [
                "pdflatex",
                "biber",
                "index",
                "glossary",
                "pdflatex",
                "pdflatex"
            ]
        },
```

- Pour voir le PDF compilé, utilisez le panneau latéral et cliquer sur "View in VSCode tab" ou utilisez le raccourics ``ctrl+alt+v```.

Pour plus d'informations :

- <https://github.com/James-Yu/LaTeX-Workshop/wiki/Compile>
- <https://github.com/James-Yu/LaTeX-Workshop/wiki/View>

### Configuration Sublime Text 3

First, you need to install the __LatexTools__ package.
Make sure to have Texlive, Summatra PDF, and ImageMagick (read the Latextools doc for more informations or possibilities).

And in Sublime, you just need to go to Preferences > Package settings > Latextools > Reset user settings to default.

And you'll then make these changes :

- Change the distro from miktex to texlive.

- Texpath should have been auto added but you can edit it to your conveniance if the Check System function doesn't tell you that everything is available.

- Go down to builder and select "script".

- In builder setings, add a "script_commands" inside your OS with these lines :

```
"windows" : { // See README or third-party documentation "script_commands" : [ "pdflatex -synctex=1 -interaction=nonstopmode -shell-escape", "biber", "makeindex -s nomencl.ist -t $file_base_name.nlg -o $file_base_name.nls $file_base_name.nlo", "makeglossaries", "pdflatex -synctex=1 -interaction=nonstopmode -shell-escape", "pdflatex -synctex=1 -interaction=nonstopmode -shell-escape" ] },
```

- Then add the option inside builder settings (not inside your OS there) : "options" : ["--shell-escape"],

That's it ! You should be able to compile with ctrl+b or ctrl+shift+b and using the "Latex - Script Builder".

If you want then to have a simpler and faster compilation system, select the "basic" builder and add the option "program": "pdflatex", inside your builder_settings.

More informations available here : <https://latextools.readthedocs.io/en/latest/install/>

Voir mon post sur tex.stackexchange pour plus d'informations : <https://tex.stackexchange.com/questions/642957/how-can-i-compile-a-complexe-document-in-sublime-text-3-with-latextools-just-lik>

## Apprendre à utiliser LaTeX

Pour apprendre à utiliser LaTeX, ce document fournis plusieurs exemples d'intégrations d'éléments pour la rédaction de documents scientifiques (figures, tableaux, équations, références, etc.).

Vous pouvez également consulter le fichier [latex_tutorial](latex_tutorial.md) pour plus d'informations.

## Licence du code

Ce code est sous licence [MIT](https://choosealicense.com/licenses/mit/).
Des informations sur la licence de ce code peuvent être trouvées dans le fichier [__LICENSE__](LICENSE) ou en suivant ce lien : [MIT License - Mathis Gauthey](https://mathisgauthey.mit-license.org/).

## Donations

### Pourquoi donner ?

Je crois en un monde où chaque logiciel dispose d'une alternative open-source maintenue par un groupe de personnes formidables pour améliorer la vie de chacun, et non par une entreprise qui ne cherche que des profits avec des marges élevées.

C'est pourquoi je mets en open-source presque tous mes projets et j'essaie d'aider autant que possible les personnes qui ont besoin d'aide pour utiliser ces projets. Bien sûr, tout cela prend du temps, du temps que je suis prêt à donner pour que vous puissiez utiliser tout cela gratuitement.

Cependant, si vous utilisez mes projets et les trouvez utiles, si vous voulez m'encourager à continuer à créer des choses, ou si vous croyez au même idéal que moi, il vous est possible de faire un don pour me permettre de continuer.

Merci beaucoup, et assurez-vous de vous amuser dans la vie o/

### Où effectuer un don ?

- <img src="https://user-images.githubusercontent.com/46576952/183624992-54add762-c94a-49f0-a1ae-5f6ab6029b60.png" width="25" height="25"> : [Sponsor @mathisgauthey on GitHub Sponsors](https://github.com/sponsors/mathisgauthey?frequency=recurring&sponsor=mathisgauthey)
- <img src="https://user-images.githubusercontent.com/46576952/183625101-1587f395-647a-44bc-b93f-d957eb3bbe43.png" width="25" height="25"> : [Donate to mathisgauthey](https://www.paypal.com/donate/?hosted_button_id=7Z9AFY6SXMCJ2)
- <img src="https://user-images.githubusercontent.com/46576952/183625101-1587f395-647a-44bc-b93f-d957eb3bbe43.png" width="25" height="25"> : [paypal.me/mathisgauthey](https://paypal.me/mathisgauthey?country.x=FR&locale.x=fr_FR)
- <img src="https://user-images.githubusercontent.com/46576952/183625042-564ff213-54a0-471c-aef4-e327be148c60.png" width="25" height="25"> : [ko-fi.com/mathisgauthey](https://ko-fi.com/mathisgauthey)
- <img src="https://user-images.githubusercontent.com/46576952/183625068-269229e4-0e11-429a-8f72-20a21657c7e1.png" width="25" height="25"> : [buymeacoffee.com/mathisgauthey](https://www.buymeacoffee.com/mathisgauthey)
