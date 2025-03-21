# Accessibilité (session 3)

## Navigation au clavier

- Les `composants interactifs` (qui a un interaction avec un autre ou a un js derrière) doivent être utilisable au clavier
- utiliser les éléments focusable nativement (liens, button, ...)
- toujours déplacer le focus là ou il fait sens
- tabindex
  - 0: focusable et tabulable (composant interactive)
  - -1: focusable mais pas tabulable
  - éviter les autres valeurs positives
- ne jamais supprimer le focus (outline: 0 ou outline: none) cf: https://www.outlinenone.com/
  - sauf si on le restyle CORRECTEMENT derrière via element:focus par exemple (attention à bien respecter le ratio de contraste)
- s'il y a des changements d'ordre niveau affichage
  - le faire côté css (flexbox par exemple)
  - la structure dom doit rester cohérente (pas d'inversion paragraphe titre par exemple)
- Lib qui détecte l'origine du focus (clavier ou souris): https://github.com/ten1seven/what-input
- https://codepen.io/okeul/pen/ZZYOgQ 
- utiliser button[type="button"] en dehors d'un formulaire
-

## Composants

- Bonne pratiques et suggestions non obligatoires: https://www.w3.org/WAI/ARIA/apg/patterns/
- Design system de l'Etat: https://www.systeme-de-design.gouv.fr/
- Cas composant `disclosure`:
  - S'il y a chargement de liste via un bouton "voir plus de ...", toujours mettre le focus sur le premier élément de la liste nouvellement chargé (éviter les infinites scrolls)
  - S'il y a suppression d'élément, il faut réflechir sur ou mettre le prochain focus
  - element <details> + <summary> (peut remplacer du js mais pas encore bien supporter partout)
- Cas custom select
  - recréeer tout un élement <select> en aria
  - focus au 1ère élément
  - déplacement avec les flèches
  - séléction en touche entrée
  - ...
- Cas custom checkbox
    - cacher visuellement la case à cocher
    - utiliser des pseudo element before et after
    - rendre visible la prise du focus en appliquant l'effet d'outline sur le sélecteur label:before
    - respecter le contraste (au moins 3)
    - ex: https://codepen.io/okeul/pen/RwpvzaP
- Cas autocompletion
  - associée à un champ de saisie (role="combobox")
  - representé par une liste déroulante d'élément
  - doit contenir un help-text en sr-only qui explique comment utiliser la liste niveau clavier
  - un élément sr-only qui dis le nombre de suggestions
  - la liste doit avoir un role="listbox" et les élément un role "option"
- Datepicker
  - complexe à rendre accessible
  - permettre la saisie au clavier avec aide à la saisie 
  - gestion des erreur
  - ordre: <label>, <input>, bloc calendrier
- Carousel
  - Mettre en premier les boutons lecture/pause
  - Pouvoir naviguer parmi les items (pas que sur le swipe): dot, flêche
  - Déplacer le focus sur l'élement nouvellement chargé après avoir cliquer sur suivant ou précédent (ne pas oublier de contextualisé les intitulés des boutons)
  - Les éléments invisibles ne doivent pas être tabulable
- Les onglets
  - Proposition aria: role="tablist" + role="tab" (pour l'enfant)
  - Proposition temesis: 
    - les onglets sont des liens ou boutons (la liste dans un ul > li)
    - le tab content avec un tabindex="-1"
    - lien de retour à l'onglet
- Popin
  - contenir un bouton de fermeture
  - un titre (h1)
  - aucune action possible sur le reste de la page
  - le focus doit être sur le bouton de fermeture à l'ouverture
  - la navigation clavier doit rester dans le modal (focus trap)
  - à la fermeture de la modal, le focus doit revenir sur l'élément declencheur de la modal
  - role="dialog" aria-modal="true"
  - si pas de titre aria-label="true"

## DataViz

- Associé les visuels complexes (chart) avec un tableau de donnée (c'est ceci qui va servir d'élément accessible)

## Tester

- Devtools
- Les extenssions
- Lecteur d'ecran (nvda, jaws)
- outils d'integration continue (axe-core, tanaguru)
- linter (axe-core)

## Ressources (youtube)

- Rob dobson: a11ycasts
- Leonie watson
- Manuel Matuzovic
- Carie Fisher
- Heydon Pickering
- Atalan: https://www.accede-web.com/notices/html-et-css/
- a11support (équivalent de caniuse mais pour le a11y)
- ...
