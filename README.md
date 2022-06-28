# Template_Rapport_Stage_Polytech_Latex
Template de rapport de stage (ou autre) en LateX utilisable à Polytech Lyon ou dans n'importe quelle école du réseau Polytech sous réserve de changer les images.
Nom du PDF final demandé à Polytech Lyon en date de la promotion 2021-2022 :

__AAAA_MM_5A_SPECIALITE_NOM_PRENOM__

Comment l'utiliser ?
Télécharger l'archive ou cloner le repo :
![image](https://user-images.githubusercontent.com/46576952/156882294-df1c6cbe-b5b8-4b1f-958f-65d4c2228846.png)

Puis l'importer et l'utiliser sur votre éditeur LateX (du plus user friendly au plus horrible à mettre en place) :
- Overleaf
- Texstudio
- VS Code
- Sublime-Text-3

<ins>Remarque :</ins> Je recommande ici d'installer TexLive. En effet, les logiciels Texstudio, VS Code et Sublime-Text-3 sont des éditeurs de texte, mais votre PC a besoin d'un compilateur LaTeX pour fonctionner.

NB : Une version exploitable a également été upload sur Overleaf : https://fr.overleaf.com/latex/templates/polytech-lyon-rapport-stage-latex/xbjcfqjgfznt
Elle n'est pas maintenue à jour contrairement à ce repo, mais il devrait déjà y avoir de quoi faire.

# Configuration TexStudio
- Dans **Compilation**, choisir le paramètre de compilation PDFLaTeX : ``pdflatex.exe -synctex=1 -interaction=nonstopmode -shell-escape %.tex``
- Dans **Production**, choisir Biber en tant que moteur de bibliographie par défaut.
- Bien penser à appuyer sur F9 pour mettre à jour le glossaire quand il est modifié avant de compiler.
- Penser également à créer un user command "Make Nomenclature" : ``makeindex -s nomencl.ist -t %.nlg -o %.nls %.nlo`` (https://www.youtube.com/watch?v=kW97Yv0-QC4)
- Compiler avec F5 pour compiler et visualiser. La compilation peut se lancer plusieurs fois pour prendre en compte la bibliographie, bien attendre qu'il soit indiqué : ``system returned with code 1 Processus terminé normalement``. Autrement, vérifier les logs et corriger les erreurs.

# Configuration VS Code
- Installer l'extension **Latex Workshop** (https://marketplace.visualstudio.com/items?itemName=James-Yu.latex-workshop)
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
                "%DOCFILE%.ist",
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
- https://github.com/James-Yu/LaTeX-Workshop/wiki/Compile
- https://github.com/James-Yu/LaTeX-Workshop/wiki/View

# Configuration Sublime Text 3
First, you need to install the **LatexTools** package.
Make sure to have Texlive, Summatra PDF, and ImageMagick (read the Latextools doc for more informations or possibilities).

And in Sublime, you just need to go to Preferences > Package settings > Latextools > Reset user settings to default.

And you'll then make these changes :

- Change the distro from miktex to texlive.

- Texpath should have been auto added but you can edit it to your conveniance if the Check System function doesn't tell you that everything is available.

- Go down to builder and select "script".

- In builder setings, add a "script_commands" inside your OS with these lines :

``"windows" : { // See README or third-party documentation "script_commands" : [ "pdflatex -synctex=1 -interaction=nonstopmode -shell-escape", "biber", "makeindex -s nomencl.ist -t $file_base_name.nlg -o $file_base_name.nls $file_base_name.nlo", "makeglossaries", "pdflatex -synctex=1 -interaction=nonstopmode -shell-escape", "pdflatex -synctex=1 -interaction=nonstopmode -shell-escape" ] },``

- Then add the option inside builder settings (not inside your OS there) : "options" : ["--shell-escape"],

That's it ! You should be able to compile with ctrl+b or ctrl+shift+b and using the "Latex - Script Builder".

If you want then to have a simpler and faster compilation system, select the "basic" builder and add the option "program": "pdflatex", inside your builder_settings.

More informations available here : https://latextools.readthedocs.io/en/latest/install/

Voir mon post sur tex.stackexchange pour plus d'informations : https://tex.stackexchange.com/questions/642957/how-can-i-compile-a-complexe-document-in-sublime-text-3-with-latextools-just-lik

# Licence
Informations disponibles dans le fichier LICENSE ou en suivant ce lien : https://mathisgauthey.mit-license.org/

# Donations
Je crois en un monde où chaque logiciel dispose d'une alternative open-source maintenue par un groupe de personnes formidables pour améliorer la vie de chacun, et non par une entreprise ne cherchant que le profit avec des marges élevées.

Je mets en open-source presque tous mes projets et j'essaie d'aider autant que possible les personnes qui ont besoin d'aide pour utiliser ces projets. Bien sûr, tout cela prend du temps, du temps que je suis prêt à consacrer pour que vous puissiez utiliser tout cela gratuitement.

Cependant, si vous utilisez mes projets et les trouvez utiles, si vous voulez m'encourager à continuer à créer des choses, ou si vous croyez au même idéal que moi, il vous est possible de faire un don.

Pour cela, tout se passe sur le bandeau à droite du projet :

![brave_V0Zg0T3uRq](https://user-images.githubusercontent.com/46576952/176141742-02eb7c41-5111-48a0-a186-7da32d072141.png)
