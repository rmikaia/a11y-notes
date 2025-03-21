# Accessibilité (session 1)

## Arbre d'accessibilité
  - consommer par techno d'assistance (TA)
  - DOM -> arbre d'accesibilité (s'appuie sur le dom mais reprend juste les éléments avec sémantique/sens/role)
  - il y aura des informations par noeud qui seront exploité par les techno d'assistance (ex: name, role)

## Limites
- Shadow dom
  - on peut faire très bien de l'accessibilité 
  - MAIS ne peut pas accéder via référence (ex: aria-labelledby) du shadow dom au light dom

## Aria
- Spécification du W3C pour ajouté une surcouche a l'html
- **Il faut ajouter en dernier recours si les balises n'ont pas de sens (span, div). Toujours privilégier le html natif (a, form)**
- ajoute : nom, role, etat, propriété
- AccName: nom accesible
  - aria-labelledby
  - aria-label
  - noeud text / alt
  - title (pas idéale)
    - Ajouté une classe générique avec les propriétés qui fait que le texte soit réstitué au TA mais que l'élément soit pas visible. (Ex: .sr-only)(https://gist.github.com/ffoodd/000b59f431e3e64e4ce1a24d5bb36034)
- Description accessible (faire attention a ne pas abuser en information)
  - aria-describedby
  - title (si il y a déjà un nom acc)

- On peut donner une sémantique à un élément qui n'en a pas (ex: role) <div role="heading" aria-level="1"> <- à éviter si possible
- annule ou écrase la sémantique d'un élément avec sémantique
- étendre les capacité d'html (ex: role="alert" -> l'augmentation de la quantité va augmenter le prix dans un autre bloc). Va mettre a jour dynamiquement les informations dans un element avec cet attr pour dire qu'une info a changé .role="alert" est un raccourci a aria-live="polite" + aria-atomic="true"
- le fait de mettre un role ne va pas forcément rendre l'élément atteignable au clavier (tab, focus, ...). Il faut ajouter tabindex="0" des fois.
- Indiquer ou on est dans une liste (ex: aria-current="true", ...)
  - peut by-passé l'utilisation de class (ex: is-active) pour privilégié l'aria
- Indiquer l'état d'un élément par exemple un bouton d'affichage du mot de passe (ex: aria-pressed)
- Indiquer l'élément courant est sélectionné dans une liste customisé différent d'une liste déroulante (ex: aria-selected)
- Indiquer qu'un élément s'est ouvert/expanded (ex: aria-expanded)
- Enrichir les formulaire (ex: aria-required, aria-invalid, aria-disabled, ...)
- Dire qu'un élément une fenetre modal (ex: aria-modal)
- Dire qu'un élément est masqué (ex: aria-hidden)

## Règle 

- RGAA: https://accessibilite.numerique.gouv.fr/methode/criteres-et-tests/
- Ne requiert pas de html valide W3C ni la déclaration du doctype mais recommandé
- Mettre l'attribut langue niveau html <html lang="fr"> ou sur un lien de switch de langue ou sur une changement de langue partiel dans le texte => pour les lecteurs d'écran et c'est bénéfique aussi pour le SEO (valeur pour l'attribut lang => https://fr.wikipedia.org/wiki/Liste_des_codes_ISO_639-1)
- si version arabe ou japonais mettre le sens de lecture (ex: dir="rtl")

## Titre (title)

- Nom de la page | nom du site (ex: Passeport | service-public.fr)
- Pour les SPA, il faut mettre à jour manuellement via le code (react/angular) le title de la page. Pareil pour le cas pagination ou panier (avec nombre d'éléments)

# Critère d'accessibilité
## Viewport (Mobile)

- ne pas empêcher le zoom (`<meta content="...maximum scale=x ... ou user scalable=no" />`)

## Régions principales de la page

Ajout d'info supplémentaire (voir redondant) pour que le site soit conforme sur tous les navigateurs

- Les zones: (landmark)
	- `<header role="banner">...`
	- `<form role="search">...`
	- `<nav role="navigation" aria-label="menu principal">...`
	- `<main role="main">...`
	- `<aside role="complementary">...`
	- `<footer role="contentinfo"> ...`
- landmark: Pour détecter les régions pricincipaux de la page https://chromewebstore.google.com/detail/landmark-navigation-via-k/ddpokpbjopmeeiiolheejjpkonlkklgp 

## Systèmes de navigation

Il faut au moins deux des systèmes de navigation suivant soit présente et accessible (fonctionnel)
- Menu de navigation
- Plan du site
- Moteur de recherche (qui index tous le contenu du site et non seulement un module en particulier)

## Contraste suffisant (couleur)

Echelle de 1 à 21 (au moins à 4.5, plus c'est grand plus c'est bien)

- https://codepen.io/ArnzWeb/full/WMdmGB 
- https://www.tpgi.com/color-contrast-checker/
- https://app.contrast-finder.org/ 
- WCAG contrast checker : https://chromewebstore.google.com/detail/wcag-color-contrast-check/plnahcmalebffmaghcpcmpaciebdhgdf

## Unité relative pour les tailles de texte

- utilisation du rem, em mais pas le pixel
- tester sur l'un des 2 zooms (graphique et texte) à 200% (les textes ne devraient pas se chevaucher, pas de pertes d'info)
- privilégier les min-width, et utilisé les unité relatif

## Html et Css

- Ne pas mettre des contenu porteur de sens dans le css (ex: via les pseudo element)
- Utiliser plutôt le font css plutôt que des images texte (pour pouvoir accéder facilement au contenu texte)
- Mettre une couleur en backup pour du texte ayant un background image (pour éviter du blanc sur du blanc si l'image ne se charge pas)
- Les propriété css suivant sera ignoré par le TA si appliqué: (+ l'attribut hidden en html5)
	- display: none
	- visibility: hidden
	- font-size: 0
- .sr-only-focusable (ex: sur un lien d'évitement)
- Pas d'élement sémantique vide
- Ne pas abuser des div et span (utiliser les éléments pour le bon role: ul pour les listes, bloquote pour les citation, ...)
- Avoir une cohérence dans les structures de titre


## Lien d'évitement (skip-link)

- Un élément premier qui permet d'aller directement au contenu (ou a d'autres endroits importants) dès arrivé sur la page quand on fait tab (ex: airbnb, github)
- Sur un site ou on a un menu avec plusieurs sous-themes, on peut vite tomber dedans et difficilement ressortir pour accéter au thème suivant. Dans ce genre de cas, un lien d'évitement est aussi important 
- Sur une map, l'accessibilité est très difficile. On exploite surtout les infos importantes dans la carte (ex: store locator, ...). Dans ce genre de cas, c'est important d'avoir un lien d'évitement pour ne pas tomber directement dans la carte et non sur l'info exploitable

## Sématinque 
- Hiérarchie de titre
- Liste ordonnées/non ordonnées
- citation bloc/en ligne

## Position courante

Mettre des infos supp sur l'élément courant (ex: un lien d'une pagination). Ca peut se faire via les techniques suivantes:
- title
- aria-label
- sr-only
- aria-current

## Outils

- Axe-core: Outils d'automatisation de test d'accessibilité: https://github.com/dequelabs/axe-core 
	- peut être mis dans un CI (et integré au niveau du site)
- lighthouse (lance le moteur axe derrière)
- wave: https://wave.webaim.org/
- Arc toolkit : https://www.tpgi.com/arc-platform/arc-toolkit/
- HeadingsMap (https://chrome.google.com/webstore/detail/headingsmap/flbjommegcjonpdmenkdiocclhjacmbi)
- Accessibility Insight (https://chrome.google.com/webstore/detail/accessibility-insights-fo/pbjjkligggfmakdaogkfomddhfmpjeni) 

## Bonne exemple de site accessible:

- service-public 