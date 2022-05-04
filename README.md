# Template_Rapport_Stage_Polytech_Latex
Template de rapport de stage (ou autre) en LateX utilisable à Polytech Lyon ou dans n'importe quelle école du réseau Polytech sous réserve de changer les images.
Nom du PDF final demandé à Polytech Lyon : 

__AAAA_MM_5A_SPECIALITE_NOM_PRENOM__

Comment l'utiliser ?
Télécharger l'archive ou cloner le repo :
![image](https://user-images.githubusercontent.com/46576952/156882294-df1c6cbe-b5b8-4b1f-958f-65d4c2228846.png)

Puis l'importer et l'utiliser sur votre éditeur LateX comme Overleaf en ligne ou le combo TexLive/TexStudio en local sur votre PC.

NB : Une version exploitable a également été upload sur Overleaf : https://fr.overleaf.com/latex/templates/polytech-lyon-rapport-stage-latex/xbjcfqjgfznt
Elle n'est pas maintenue à jour contrairement à ce repo.

# Configuration TexStudio
- Dans **Compilation**, choisir le paramètre de compilation PDFLaTeX : ``pdflatex.exe -synctex=1 -interaction=nonstopmode -shell-escape %.tex``
- Dans **Production**, choisir Biber en tant que moteur de bibliographie par défaut.
- Bien penser à appuyer sur F9 pour mettre à jour le glossaire quand il est modifié avant de compiler.
- Penser également à créer un user command "Make Nomenclature" : ``makeindex -s nomencl.ist -t %.nlg -o %.nls %.nlo`` (https://www.youtube.com/watch?v=kW97Yv0-QC4)
- Compiler avec F5 pour compiler et visualiser. La compilation peut se lancer plusieurs fois pour prendre en compte la bibliographie, bien attendre qu'il soit indiqué : ``system returned with code 1 Processus terminé normalement``. Autrement, vérifier les logs et corriger les erreurs.

# Configuration Sublime Text 3
Voir mon post sur tex.stackexchange : https://tex.stackexchange.com/questions/642957/how-can-i-compile-a-complexe-document-in-sublime-text-3-with-latextools-just-lik

# Licence
Informations disponibles dans le fichier LICENSE ou en suivant ce lien : https://mathisgauthey.mit-license.org/
