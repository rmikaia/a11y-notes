# Accessibilité (session 2)

## Liens

- type:
  - Liens internes
  - Liens externes
  - Liens ancres
- attr href avec une valeur non vide
- doit contenir quelques choses (text, img, ...)
- Lien non explicites hors contexte (lire la suite, en savoir plus)
  - explicité par un attribut `title` (valeur + contexte). Ex: Lire la suite de l'article toto
  - important de reprendre la valeur (Lire la suite)
- Lien avec contexte explicite (le contenu du lien est explicite / parlant) ou si le lien est contenu dans un conteneur (p, ul>li, hn qui le précède, th associé ou td)
- attribut title
- aria-label ou aria-labelledby
- sr-only
- cas ou un bloc de contexte contienne plusieurs lien cliquable
  - etendre le descriptif du lien sur tous le bloc
  - 3 solution (en css, en javascript, en html)
  - css > js > html
  - 
  - voir: https://codepen.io/okeul/full/aGxGgJ
- Lien composite (avec image)
  - on ignore via aria-hidden="true" et focusable="false" (ex: sur du svg). Le problème du focusable c'est que sur IE
- Document en téléchargement, indiqué le format et le poids dans le lien (recommandé)

## Image

- alt obligatoire pour éviter que la TA lise toute la src de l'image (ex: https://statics/image.png)
- décorative (alt vide) => il faut quand même voir par rapport au contexte si l'image est porteur d'information ou non
- svg décorative: mettre un aria-hidden="true"
  - vérifier s'il y a pas title et desc (ainsi que sur les éléments enfant)
  - pareil pour les aria-labelledby, aria-label, ...
  - la lecture du svg peut être inaudible sans mesure spécifique
- informative: indiqué dans le alt (Il faut être bref et ne pas être redondant ex: alt="Logo Visa")
- bg css: non conforme
  - solution: mettre un sr-only
- les icon-font (fontawesome, ...): peut être problématique en accessibilité (pour éviter que le TA vocalise le contenu du content dans le css)
  - solution: mettre un aria-hidden="true" + sr-only
- image lien: spécifier via un sr-only la nature du lien image
- captcha: spécifié dans le alt que c'est un captcha
  - d'après les sondages (webaim), c'est l'élément qui pose le plus de problème pour les gens déficients
  - essayer de trouver un compromis avec l'équipe sécurité entre le captcha et l'accessibilité
- Image légendé (galerie d'image): texte associé à une image
  - figure et figcaption
  - il faut mettre le role figure
  - figure[aria-label] doit être égale au contenu du figcaption
- Image avec beaucoup d'informations
  - il faut mettre une description bref dans un alt
  - et explicité tous les éléments de l'image dans la page
- canvas (voir site longchamp)
  - ajout d'aria-label avec la description
  - ou ajouter un texte à l'interieur du canvas
  - si c'est décorative, ajouter un aria-hidden="true"
  - ajouter un role img
  - cette règle est valable sur les svg informative

## Formulaires

- liaison label champs
  - le for id est obligatoire: label[for="my-id"] <-> input#my-id
  - label explicite: label + input
  - label implicite: label > input
- indiquer les champs obligatoire via l'attribut required (ou aria-required="true")
- placeholder: sans label, le placeholder ne permet pas d'être conforme en accessibilité. Le placeholder ça doit être à titre descriptif mais ne remplace pas le label.
  - floating-label: peut être un compromis
  - ajouter un title si jamais impossible d'ajouter le label (ex: bras de fer avec le designer ou un champs de recherche)
- autocompletion: utiliser via l'attribute autocomplete et renseigner la bonne valeur (cf )
- regroupement de champs via fieldset > legend
  - pose des problèmes d'accessibilité (s'il y a imbrication de fieldset)
  - solution: utiliser un role="group" + aria-labelledby
- Format de saisie dans le label (aide à la saisie)
  - incorporé dans le label
  - soit si c'est en dehors (dans un p par exemple), on lie avec aria-describedby
- Erreurs: 
  - soit par champs (inline)
    - déplacer le focus sur le premier champs en erreur (el.focus() en js)
      - chrome devtools (cliquer sur l'icone oeil > taper document.activeElement)
    - ou aria-describedby (peut prendre ) si l'erreur est en dehors du label
  - soit par block 
    - déplacer le focus sur le block
    - il faut ajouter l'attribut tabindex="-1" pour que le div du block puisse être focusable
  - il faut mettre à jour le title de page s'il y a chargement de page

## Tableaux

- simple
  - déclarer les entêtes simple (thead et th)
  - il faut toujours mettre un titre au tableau via l'élément <caption> qui peut être en sr-only (non-visible)
- complexe
  - tableaux avec double entrée 
    - il faut metre les scope="col" (entête de colonne) et scope="row" (entête de rangé)
- entêtes irrégulières (avec des fusions, ...)
  - on utilise les attributs headers et id à la place des attributs scope pour relier cellules et entêtes
- tableaux de mise en forme (#vintage)
  - ajouter un role="presentation"
  - ne pas utiliser les éléments propres au tableaux (caption, th, thead, tfoot, scope, headers, ...)

## iframe

- iframe affiché à l'utilisateur: `title` obligatoire avec une valeur pertinente
- iframe technique (non-visible par l'utilisateur) => on ignore (display:none, hidden, aria-hidden="true")

## vidéo, audio

- il y a plusieurs enjeux d'accessibilité 
- il faut qu'il y a les boutons de controle (notamment pause) <- l'accessibilité stipule que si la vidéo se joue plus de 5s
- titre
- éviter le déclenchement automatique (autoplay) => n'est pas une règle d'accessibilité
- controles accessibles aux claviers
- compatible lecteur d'ecran
- lancer/arreter les sous titres/audio-description
- play/pause ou stop
- controler le volume
- transcription (obligatoire si la vidéo est porteuse d'info)
  - utilisation `aria-expanded` (true ou false) sur le button + l'affichage du contenu de la transcription
  - si on dynamise le contenu du bouton en "Afficher la transcription" ou "Masquer la transcription" selon le contexte, il n'y aura pas besoin du `aria-explanded` (donc soit l'un soit l'autre)
- Limitation temporelle (< 20h)
  - ex: prix sur un site de réservation de billets, les prix peuvent changer d'une période à l'autre
  - session expirée (prévenir l'utilisateur avant une deconnexion auto)
  - l'utilisateur doit pouvoir annuler, ajuster, étendre la durée de la limitation

# Site

- https://webaim.org/projects/screenreadersurvey10/
- https://www.hteumeuleu.com/ (email accessible)
- 