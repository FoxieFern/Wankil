* Classement par ordre alphabétique des [épisodes de L&T](https://www.youtube.com/c/wankilfr) publiés sur la chaîne principale : **[videos-sorted-by-title.md](videos-sorted-by-title.md)**
* Correspondances entre les VOD publiées sur la [chaîne secondaire](https://www.youtube.com/user/terracid) et les épisodes de L&T : **[videos-linked-to-vod.md](videos-linked-to-vod.md)**
* Liste des musiques utilisées dans les épisodes de L&T : **[music-in-wankil-videos.md](music-in-wankil-videos.md)**

Mémo commandes :
```
Titres
* grep -o 'title="[^"]\+"' [HTML.txt] | awk '{ gsub ("title=", "", $0); print}' | sort

Miniatures
* grep -o 'href="/watch?v=[^"]\+"' [HTML.txt] | awk -F"=" '{print $NF}' | tr -d '"' | uniq > listURL.txt
* for url in `cat listURL.txt`; do echo $URL; curl http://img.youtube.com/vi/"$url"/sddefault.jpg > "$url".jpg; done
* for i in `ls *.jpg`; do convert $i -trim -bordercolor Black $i; done
* montage -geometry +1+1 -tile 5x -background none -mode concatenate $(ls *.jpg | shuf -n 50) resultat.jpg
```
