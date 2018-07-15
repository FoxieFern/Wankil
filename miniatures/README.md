_[<<< Page précédente - Wankil](https://github.com/nbrisset/Wankil)_

_Disclaimer : Attention ! Warning ! Achtung ! Soyez extrêmement vigilants lorsque vous [copiez-collez des lignes de commande](https://thejh.net/misc/website-terminal-copy-paste) depuis Internet. Pensez bien à tourner sept fois vos doigts au-dessus de votre clavier avant d'appuyer sur Entrée._ En quelques lignes de commande et à l'aide du logiciel [ImageMagick](https://imagemagick.org/script/index.php), il est possible de faire des choses plutôt sympas avec les miniatures de vidéos YouTube.

* Récupération et stockage des identifiants YouTube de chaque vidéo

```grep -o 'href="/watch?v=[^"]\+"' [HTML.txt] | awk -F"=" '{print $NF}' | tr -d '"' | uniq > listURL.txt```

* Téléchargement des miniatures (en HD) de chaque vidéo

```nb=1; for url in $(cat listURL.txt); do echo $URL; curl http://img.youtube.com/vi/"$url"/sddefault.jpg > $nb.jpg; ((nb++)); done```

* Listing des images à supprimer (fichier corrompu, échec de téléchargement...)

```find . -name "*.jpg" -size -2k```

* Rognage des bordures noires de toutes les miniatures

```for i in $(ls *.jpg); do convert $i -trim -bordercolor Black $i; done```

* Assemblage des miniatures, ici [50 miniatures choisies au hasard](thumbs_random50.jpg) réparties par lignes de 5

```montage -geometry +1+1 -tile 5x -background none -mode concatenate $(ls *.jpg | shuf -n 50) thumbs_random50.jpg```

* Assemblage des miniatures, ici [les 30 premières miniatures de la liste](thumbs_first30.jpg) réparties par lignes de 6

```montage -geometry +1+1 -tile 6x -background none -mode concatenate $(ls *.jpg | sort -V | head -n 30) thumbs_first30.jpg```
