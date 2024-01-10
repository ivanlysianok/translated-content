---
title: "Element : évènement beforeinput"
slug: Web/API/Element/beforeinput_event
l10n:
  sourceCommit: eb7517609a230a62f37dd4270867586b684793fa
---

{{APIRef}}

L'évènement DOM **`beforeinput`** est déclenché quand la valeur d'un élément [`<input>`](/fr/docs/Web/HTML/Element/input) ou [`<textarea>`](/fr/docs/Web/HTML/Element/textarea) est sur le point d'être modifié. À la différence de [l'évènement `input`](/fr/docs/Web/API/Element/input_event), `beforeinput` n'est pas déclenché pour les éléments [`<select>`](/fr/docs/Web/HTML/Element/select). Cet évènement s'applique également aux éléments ayant l'attribut [`contenteditable`](/fr/docs/Web/API/HTMLElement/contentEditable) actif, et à tout élément quand [`designMode`](/fr/docs/Web/API/Document/designMode) est actif.

Cela permet aux applications web de surcharger l'édition de texte avant que le navigateur ne modifier l'arbre du DOM, offrant ainsi un meilleur contrôle sur les évènements de saisie pour améliorer les performances.

Dans le cas de `contenteditable` et `designMode`, la cible de l'évènement est **l'hôte d'édition**. Si ces propriétés s'appliquent à plusieurs éléments, l'hôte d'édition est le plus proche ancêtre dont le parent n'est pas éditable.

> **Note :** Toute modification apportée par une utilisatrice ou un utilisateur ne déclenche pas nécessairement `beforeinput`. De plus, l'évènement peut être déclenché mais ne pas être annulable&nbsp;: cela se produit lorsque l'autocomplétion est utilisée, qu'une correction proposée par un correcteur est acceptée, ou qu'un remplissage automatique est réalisé par un gestionnaire de mots de passe, qu'un [IME](/fr/docs/Glossary/Input_method_editor) est utilisé, etc. Les détails varient d'un navigateur à l'autre et d'un système d'exploitation à un autre. Pour surcharger l'édition en question dans tous les cas, le code devra gérer l'évènement [`input`](/fr/docs/Web/API/Element/input_event) et éventuellement annuler les modifications qui n'auraient pas été gérées par le gestionnaire `beforeinput`.

## Syntaxe

On utilisera le nom de l'évènement pour les méthodes [`addEventListener()`](/fr/docs/Web/API/EventTarget/addEventListener), ou on définira une propriété de gestion d'évènement.

```js
addEventListener("beforeinput", (event) => {});

onbeforeinput = (event) => {};
```

## Type d'évènement

`beforeinput` est un évènement [`InputEvent`](/fr/docs/Web/API/InputEvent) et hérite de [`UIEvent`](/fr/docs/Web/API/UIEvent).

{{InheritanceDiagram("InputEvent")}}

## Propriétés de l'évènement

_Cette interface hérite des propriétés de ses parents, [`UIEvent`](/fr/docs/Web/API/UIEvent) et [`Event`](/fr/docs/Web/API/Event)._

- [`InputEvent.data`](/fr/docs/Web/API/InputEvent/data) {{ReadOnlyInline}}
  - : Renvoie une chaîne de caractères avec les caractères insérés. Il peut s'agir d'une chaîne vide si la modification n'insère pas de texte (c'est le cas lorsqu'il n'y a que des caractères supprimés par exemple).
- [`InputEvent.dataTransfer`](/fr/docs/Web/API/InputEvent/dataTransfer) {{ReadOnlyInline}}
  - : Renvoie un objet [`DataTransfer`](/fr/docs/Web/API/DataTransfer) contenant des informations à propos du texte riche ou simple qui est ajouté ou supprimé du contenu éditable.
- [`InputEvent.inputType`](/fr/docs/Web/API/InputEvent/inputType) {{ReadOnlyInline}}
  - : Renvoie le type de changement pour le contenu éditable, comme l'insertion, la suppression ou la mise en forme.
- [`InputEvent.isComposing`](/fr/docs/Web/API/InputEvent/isComposing) {{ReadOnlyInline}}
  - : Renvoie un booléen qui indique si l'évènement est déclenché [`compositionstart`](/fr/docs/Web/API/Element/compositionstart_event) et avant [`compositionend`](/fr/docs/Web/API/Element/compositionend_event).

## Exemples

### Détection de la fonctionnalité

La fonction qui suit renvoie `true` si `beforeinput` et donc `getTargetRanges` sont pris en charge.

```js
function isBeforeInputEventAvailable() {
  return (
    window.InputEvent &&
    typeof InputEvent.prototype.getTargetRanges === "function"
  );
}
```

### Une journalisation simple

Dans cet exemple, on affiche la valeur courante de l'élément avant qu'elle soit remplacée immédiatement par la nouvelle valeur appliquée à l'élément [`<input>`](/fr/docs/Web/HTML/Element/input).

#### HTML

```html
<input placeholder="Saisissez un texte quelconque" name="name" />
<p id="values"></p>
```

#### JavaScript

```js
const input = document.querySelector("input");
const log = document.getElementById("values");

input.addEventListener("beforeinput", updateValue);

function updateValue(e) {
  log.textContent = e.target.value;
}
```

#### Résultat

{{EmbedLiveSample("")}}

## Spécifications

{{Specifications}}

## Compatibilité des navigateurs

{{Compat}}

## Voir aussi

- L'évènement associé [`input`](/fr/docs/Web/API/Element/input_event)
