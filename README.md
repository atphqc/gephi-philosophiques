# gephi-philosophiques
Les visualisations des matrices auteurs-formes pour la revue Philosophiques. Les visualisations sont réalisées sur [Gephi](https://gephi.org/), puis exportées en HTML5 grâce à l'extension [SigmaExporter](https://gephi.org/plugins/#/plugin/sigmaexporter). <br/><br/>

## Structure des URLs pour afficher les visualisations
```
https://atphqc.github.io/gephi-philosophiques/[nombre de formes par auteur]-formes-[types de formes]/[décennie]
```
   
Nombre de formes par auteurs : 5, 10 ou 20   
Types de formes : simples ou complexes   
Exemple : https://atphqc.github.io/gephi-philosophiques/5-formes-simples/2000/
<br/><br/>

## À faire
- [ ] finir une première version de toutes les visualisatons,
- [ ] repérer et éliiminer le bruit,
- [ ] écrire les titres, descriptions, etc. 
- [ ] ajouter les articles de 2024 au corpus.
<br/><br/>

## Recréer les visualisations 
### Dans Gephi
- Importer la matrice dans Gephi.
- Dans le laboratoire de données :   
	- ajouter deux colonnes dans le tableau de noeuds (nodes), une colonne « type » pour définir le type du noeud (auteur ou forme) et une colonne « color » pour personaliser la couleur (#548ac2 pour les auteurs, #ff4242 pour les formes),
	- ajouter une colonne pour personliser la couleur dans le tableaux des liens (edges), tous les liens sont de couleur #548ac2.
- Dans la vue d'ensemble :
	- appliquer les couleurs définies dans le laboratoire de données grâce aux extensions « [Give color to nodes](https://gephi.org/plugins/#/plugin/givecolortonodes) » et « [Give color to edges](https://gephi.org/plugins/#/plugin/givecolortoedges) »,
	- classer les noeuds par degré, les tailles de 5 à 50 fonctionnent bien pour les plus petites visualisation, il faut adapter selon la visualisation,
 - appliquer l'algorithme Yifan Hu,
 - désemcombrer la visualisation en utilisant les options de spatialisation d'expansion, de déchevauchement et d'ajustement des labels.
- Exporter en SigmaJS Template, grâce à l'extension « [SigmaExporter](https://gephi.org/plugins/#/plugin/sigmaexporter) ».

### Dans les fichiers exportés
Il faut personnaliser certains fichiers ou répertoires.

#### Dans ```config.json```
- changer le titre et la description courte de la visualisation
- edgeLabel : "Auteur.e",
- colorLabel : "Forme",
- malgré le fait qu'on enlève le node du HTML et du CSS, ne pas l'enlever du config.json, pour une raison obscure, ça ruine tout. Mettre "?" ou un espace,
- defaultEdgetype : "line",
- labelThreshold : 3 ou 4 dépendant de la grosseur, voire 5 à 7 pour les globales,
- maxEdgeSize : 0.5 (ou 0.25 si grande visualisation), 
- minEdgeSize : 0.5 (ou 0.25 si grande visualisation),
- minNodeSize : 1
- maxNodeSize : 10 (ou 7 si grande visualisation)
  
 #### Dans ```index.html```
- ***changement du titre de la page dans l'élément html ```<title>```, à faire à chaque fois !!!***.
- traduction en français des textes,
- retrait ou mise en commentaire du code qui ne servait pas :  le ```<div id="developercontrainer">``` qui prenait trop d'espace et l'élément ```<dt class="node">``` de la légende dont nous n'avons pas besoin, puisque nous avons seulement deux éléments dans la légende (auteur et forme). 

#### Dans le dossier ```images```
- ajouts des images des points de couleurs pour la légende (auteur et forme) et du logo d'érudit dans le dossier pour leur utilisation dans le CSS. 

#### Dans ```style.css```
- intégrer les images des points de couleurs pour la légende (auteur et forme)
	- J'ai remplacé les images des éléments html avec les classe ```edge``` et ```color``` par les images qui représentent la couleur des auteurs et des formes. Ces éléments se trouvent la légende (l'élément html div avec le id ```mainpanel```, qui est le id utilisé dans le CSS plutôt que le id ```legend```, utilisé ailleurs).
	- Le CSS inutilisé, le ```background-position``` et l'élément avec la classe ```node``` -- dont nous n'avons pas besoin, car nous avons seulement deux éléments à la légendes -- ont été mis en commentaire.
 
