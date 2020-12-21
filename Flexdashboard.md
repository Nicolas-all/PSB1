---
title: "Flexdashboard Tutorial"
output:
  word_document: default
  html_document: default
  pdf_document: default
---

---


```{r setup, include=FALSE}
knitr::opts_chunk$set(echo = TRUE)
```  

# Premier pas

*Les tableaux de bord ou "Dashboard" constituent des outils graphiques qui sont très souvent utilisés pour répresenter de façon simple et parlante la donnée. C'est un moyen de visualisation très puissant qui permet de regrouper un ensemble de données très variées, et réside au coeur des métiers de la donnée.  
En tant qu'étudiants en MSc Data Management au sein de l'école Paris School of Business, il est bien évidemment important pour nous, et même essentiel de pouvoir présenter les informations clefs de façon claire et compréhensible de tous.
Il existe un multitude d'outils et de logiciels pour çela, et le package R, flexdashboard en est un exemple parfait.*


&nbsp;

Avant toute chose, il est nécessaire d'installer le package "flexdashboard": 

```{r, eval=FALSE}
install.packages("flexdashboard")
library(flexdashboard)
```

Ensuite, pour créer un flexdashboard, il faut créer un document R avec le format output : "flexdashboard::flex_dashboard".  
Il est également possible de le faire sur RStudio en utilisant la boîte de diaogue : File –> New File –> Rmarkdown –> From Templates –> Flex Dashboard.

![Téléchargement impossible](C:/Users/marko/OneDrive/Bureau/Flexdashboard tuto/boite_de_dialogue.jpg)  
Cela va permettre de créer un fichier template dashboard de ce genre :

![](C:/Users/marko/OneDrive/Bureau/Flexdashboard tuto/Test_dashboard.PNG)  

Appuyez sur le bouton Knit afin d'afficher le rendu:  

![](C:/Users/marko/OneDrive/Bureau/Flexdashboard tuto/visuel_dashboard.PNG)  

&nbsp;

Bravo !! Vous venez de créer votre premier dashboard interactif. Il est vrai qu'il peut paraître un peu simpliste, mais le squelette de votre futur dashboard est bel et bien là !  
Essayons de voir les différentes fonctionnalités que vous offre `flexdashboard`pour structurer et garnir votre tableau de bord.

&nbsp;

# Les basiques du packages  

## La disposition  

Flexdashboard va vous permettre de personnaliser vos visualisations avec énormément de liberté. A commencer par la façon dont vous voulez disposer vos graphiques   

#### En colonnes, ou en lignes  

Comme vous avez pu le constater plus haut, par défaut les dashboards sur markdown se présente en colonnes, et les graphiques sont empilés verticalement dans chacune des colonnes.  

Toutefois vous avez également la possibilité de choisir d'orienter vos tableaux de boards en lignes. POur cela il vous suffit de le spécifier dans l'en tête en modifiant l'option orientation par **rows**.  


<style>
.column-left{
  float: left;
  width: 50%;
  text-align: left;
}
.column-right{
  float: right;
  width: 50%;
  text-align: right;
}
</style>

<div class="column-left">
![](C:/Users/marko/OneDrive/Bureau/Flexdashboard tuto/dashboard_colonne.jpg)
</div>
<div class="column-right">
![](C:/Users/marko/OneDrive/Bureau/Flexdashboard tuto/dashboard_row.jpg)  

</div>  


#### **Défiler** pour naviguer  

Les graphiques flexdashboard sont générés de façon à ce qu'ils remplissent automatiquement la hateur du navigateur. Vous vous rendrez rapidement compte que si vous avez un grand nombre de graphique l'affichage ne va plus du tout être optimal.  
Flexdashboard vous donne la possibité de pouvoir défiler grâce à l'option vertical_layout dans l'en-tête, plutôt que d'avoir à tout insérer sur la même page. Cela permet de conserver la hauteur naturelle de vos graphiques, et de défiler la page si nécessaire pour naviguer à travers les graphs.  

![](C:/Users/marko/OneDrive/Bureau/Flexdashboard tuto/dashboard_scrolling.jpg)  


#### Organiser en **onglets**  

Une autre astuce d'affichage que vous offre ce package est la possibilité d'organiser vos graphiques dans des tabsets.  
Cela peut paraître bien pratiquer si vous souhaiter représenter plusieurs éléments dans une même ligne ou colonne, et vous évitera de vous perdre dans en essayant d'adapter tout sur un seul et même écran.  
Dans de nombreux cas, les onglets sont une meilleure solution que le *vertical_layout: scroll* pour afficher un grand nombre de composants, et rendent la navigation plus simple.  

Pour mettre en page une ligne ou une colonne sous forme de tabset, il vous suffit d'ajouter l'attribut *{.tabset}* dans l'en-tête de section :


![](C:/Users/marko/OneDrive/Bureau/Flexdashboard tuto/dashboard_tabset.jpg)  

#### Ajuster la taille  

La grande diversité des graphiques que vous pourrez exploiter vont parfois vous obliger à revoir les dimensions de ces derniers afin de mettre en avant certains éléments, ou bien pour ajuster et corriger l'affichage d'autres.  
Vous pouvez modifier le dimensionnement par défaut en appliquant les attribut *data-widht* et *data-height* aux lignes, aux colonnes ou même directement aux graphique concernés. Ces attributs permettent d'ajuster les dimensions (de 0 à 1000) des éléments sur la page en fonction de vos préférences.  

![](C:/Users/marko/OneDrive/Bureau/Flexdashboard tuto/ajustement_taille.PNG)  

#### Organiser en pages  

Si vous souhaitez inclure plus d'une poignée de graphiques dans un dashboard, vous avez la possiblité de le diviser en plusieurs pages. Pour définir une page il vous suffit d'utiliser un en-tête de démarquage comme cela *(================)*.  
Chaque page aura son propre onglet de navigation dans la barre supérieure.  

![](C:/Users/marko/OneDrive/Bureau/Flexdashboard tuto/page_organisation.PNG) 


## Les composants  

#### Texte et annotations  

Si vous voulez inclure des remarques ou des explications supplémentaires dans votre tableau de bord, vous pouvez le faire de différentes façon. Vous pouvez inclure du contenu en haut de la page avant l'introduction des sections du dashboard ou alors définir des sections d'annotations dans le dashboard même. 

![](C:/Users/marko/OneDrive/Bureau/Flexdashboard tuto/section_texte.PNG)
![](C:/Users/marko/OneDrive/Bureau/Flexdashboard tuto/section_texte_exemple.PNG)  

#### HTML Widgets  

Le frameword htmlwidgets va permettre d'améliorer le visuel des graphique de votre dashboard. Les graphiques basés sur htmlwidgets sont parfaits pour une utilisation avec flexdashboard car ils peuvent se redimensionner de manière dynamique et s'intégreront parfaitement dans votre dashboard. 
Les widgets html incluent :

1. **Leaflet**, une bibliothèque permettant de créer des cartes dynamiques. 

2. **dygraphs**, fournit des fonctionnalités riches pour la création de séries de données chronologiques intéractives.  

3. **plotly**, qui grâce à son interface ggplotly permet de convertir facilement vos graphiques ggplot2 en une version Web intéractive.  

4. **rbokeh**, une interface vers Bokeh, un puissant framework pour la création de tracés Web  


#### Graphiques R  

Vous pouvez également utiliser n'importe quel graphique créé avec des graphiques R standard, avec flexdashboard.  
Dans les tableaux de bord dynamique (shiny), ces graphiques sont automatiquement dimensionnés pour s'adapter à leurs emplacements.  


#### Des tables  

Vous avez aussi la possibilité d'inclure des données tabulaires dans flexdashboards de deux façons :
* En tant que simple affichage tabulaire.
* En tant que DataTable qui inclut le tri, le filtrage et la pagination.  

#### Les boîtes de valeurs  

Parmis tout les affichages possibles, on retrouve aussi des valeurs simples incluent dans des boîtes de valeur.  
Vous pouvez utiliser la fonction valueBox afin d'afficher des valeurs unique avec un titre et une icône si nécessaire. 

<style>
.column-left{
  float: left;
  width: 50%;
  text-align: left;
}
.column-right{
  float: right;
  width: 50%;
  text-align: right;
}
</style>

<div class="column-left">
![](C:/Users/marko/OneDrive/Bureau/Flexdashboard tuto/valuebox_code.PNG)
</div>

<div class="column-right">
![](C:/Users/marko/OneDrive/Bureau/Flexdashboard tuto/dashboard_boite.jpg)  

</div>  



#### Des jauges 

Les jauges permettent d'afficher les valeurs sur un compteur dans une plage spécifiée.  

<style>
.column-left{
  float: left;
  width: 50%;
  text-align: left;
}
.column-right{
  float: right;
  width: 50%;
  text-align: right;
}
</style>

<div class="column-left">
![](C:/Users/marko/OneDrive/Bureau/Flexdashboard tuto/gauge_code.PNG)

</div>

<div class="column-right">
![](C:/Users/marko/OneDrive/Bureau/Flexdashboard tuto/dashboard_jauges.jpg)  

</div>  


# Optimiser ses dashboards avec Shiny  

### A quoi ça sert ?  

En utilisant Shiny avec flexdashboard, vous pouvez créer des tableaux de bord qui permettent aux utilisteurs de modifier les paramètres sous-jacents et de voir les résultats de façon immédiate.Cela se fait en ajoutant *runtime: shiny* à un flexdashboard standard, puis en ajoutant un ou plusieurs contrôles d'entrée et / ou expressions réactives qui pilotent dynamiquement l'apparence des composants dans le dashboard.  
L'utilisation de Shiny avec flexdashboard transforme un rapport R Markdown statique en un document interactif. Il est important de noter que les documents interactifs doivent être déployés sur un serveur Shiny pour être largement partagés (alors que les documents statiques R Markdown sont des pages Web autonomes qui peuvent être jointes à des e-mails ou servies à partir de n’importe quel serveur Web standard).

#### Pour commencer avec Shiny  

Les étapes requises pour ajouter des composants Shiny à un tableau de bord flex sont les suivantes:  

1. Ajouter *runtime: shiny* aux options déclarées en haut du document (avant-propos YAML).  

2. Ajoutez l'attribut *{.sidebar}* à la première colonne du tableau de bord pour en faire un hôte pour les contrôles d'entrée Shiny.  

3.Ajoutez des entrées et sorties Shiny selon vos besoins.  

4.Lorsque vous incluez des graphiques, assurez-vous de les encapsuler dans un call à renderPlot. Ceci est important non seulement pour répondre de manière dynamique aux modifications, mais également pour s'assurer qu'ils sont automatiquement redimensionnés lorsque leur emplacement change. 

#### Un exemple simple  

![](C:/Users/marko/OneDrive/Bureau/Flexdashboard tuto/shiny_code.PNG)  

![](C:/Users/marko/OneDrive/Bureau/Flexdashboard tuto/shiny_exemple.PNG)  



&nbsp;

Vous avez maintenant tout les prérequis pour commencer à réaliser vos premiers dashboard intéractifs. C'est un outil non négligeable qui fera que vous vous démarquerez en montrant de façon claire et simple des données aussi hétérogènes soient-elles.  
C'est en forgeant que l'on devient forgeron, alors à vos commandes.  


## Bibliographie  

* http://rstudio.github.io/leaflet/ 
* https://delladata.fr/dashboard-r/ 
* https://rmarkdown.rstudio.com/flexdashboard/shiny.html#advanced

















