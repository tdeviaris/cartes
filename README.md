# cartes

Pyramides de tuiles Deep Zoom des cartes anciennes présentées sur
[French Names in Australia](https://www.frenchnamesaustralia.com/) — publiées par GitHub Pages
et affichées par `map-viewer.html` du site principal.

Ce dépôt ne contient que des images : aucun code, aucune page.

## Contenu

| Dossier      | Carte                                              | Dimensions         | Niveaux | Tuiles |
|--------------|----------------------------------------------------|--------------------|---------|--------|
| `freycinet/` | Carte générale de la Nouvelle Hollande (1808–1811)  | 20 135 × 13 078 px | 16      | 5 515  |
| `flinders/`  | General Chart of Terra Australis or Australia (1814) | 23 305 × 17 002 px | 16      | 8 279  |

## Fonds géoréférencés

`fonds/<carte>/{z}/{x}/{y}.webp` : les mêmes cartes, mais calées sur leur quadrillage gravé et
retaillées en tuiles Web Mercator (norme XYZ), pour se superposer à une carte moderne dans
Leaflet, QGIS ou MapLibre. Elles alimentent le sélecteur de fond de `map.html`.

| Dossier            | Zooms | Tuiles | Calage                                                        |
|--------------------|-------|--------|---------------------------------------------------------------|
| `fonds/freycinet/` | 3 à 9 | 8 760  | quadrillage gravé, rectifié par surfaces de Coons ; contrôle sur le tropique du Capricorne à 0,2′ |

Au-delà du zoom 9, la couche est agrandie (`maxNativeZoom: 9`). Les longitudes de Freycinet
sont comptées depuis Paris : on ajoute 2°20′14″ pour passer à Greenwich, d'où les bornes
`[[-45, 97.34], [-5, 167.34]]`. La méthode et les contrôles sont détaillés dans le
`LISEZMOI.md` de `Cartes anciennes/fond_leaflet_freycinet/`, qui conserve aussi les scripts
de calage.

## Convention

Une carte par dossier, au format Deep Zoom (DZI) :

    <carte>/<carte>.dzi          descripteur (dimensions, format, taille des tuiles)
    <carte>/<carte>_files/<niveau>/<colonne>_<ligne>.jpg

La visionneuse embarque les dimensions de chaque carte et n'appelle donc jamais le `.dzi` :
seules les tuiles sont téléchargées, comme de simples images. Le `.dzi` est conservé pour
les autres lecteurs Deep Zoom.

## Ajouter une carte

    python3 tiler.py          # voir « Cartes anciennes/visionneuse_freycinet/tiler.py »

puis déposer `<carte>.dzi` et `<carte>_files/` dans un nouveau dossier `<carte>/`, et déclarer
la carte dans `CARTES` au début de `map-viewer.html`. Les tuiles ne changent jamais une fois
générées : un seul envoi suffit.

## Sources et licence

Les numérisations proviennent de la [David Rumsey Map Collection](https://www.davidrumsey.com/)
et sont diffusées sous licence **CC BY-NC-SA 3.0** : usage non commercial, avec mention de la
source. Chaque carte cite la sienne dans le cartel de la visionneuse.
