---
title: "Element : évènement input"
slug: Web/API/Element/input_event
l10n:
  sourceCommit: eb7517609a230a62f37dd4270867586b684793fa
---

{{APIRef}}

L'évènement **`input`** est déclenché lorsque la valeur (l'attribut `value`) d'un élément [`<input>`](/fr/docs/Web/HTML/Element/input), [`<select>`](/fr/docs/Web/HTML/Element/select), ou [`<textarea>`](/fr/docs/Web/HTML/Element/textarea) a été modifié par une action directe de l'utilisatrice ou de l'utilisateur (par exemple en saisissant du texte ou en cochant une case).

Cet évènement s'applique également aux éléments avec [`contenteditable`](/fr/docs/Web/API/HTMLElement/contentEditable) actif, et à tous les éléments lorsque [`designMode`](/fr/docs/Web/API/Document/designMode) est actif. Dans ces deux cas, la cible de l'évènement est _l'hôte d'édition_. Si ces propriétés s'appliquent à plusieurs éléments, l'hôte d'édition correspond à l'élément étant le plus proche ancêtre dont le parent n'est pas éditable.

Pour les éléments `<input type=checkbox>` or `<input type=radio>`, l'évènement `input` devrait être déclenché dès que la personne active le contrôle (voir [la spécification HTML](https://html.spec.whatwg.org/multipage/input.html#the-input-element:event-input-2)). Toutefois, cela n'a pas toujours été le cas. Vérifiez les informations de compatibilité ou utilisez l'évènement [`change`](/fr/docs/Web/API/HTMLElement/change_event) pour ces types d'éléments.

Pour les éléments [`<textarea>`](/fr/docs/Web/HTML/Element/textarea) et les éléments [`<input>`](/fr/docs/Web/HTML/Element/input) acceptant du texte (`type=text`, `type=tel`, etc.), l'interface de l'évènement est [`InputEvent`](/fr/docs/Web/API/InputEvent)&nbsp;; pour les autres, l'interface est [`Event`](/fr/docs/Web/API/Event).

L'évènement `input` est déclenché à chaque fois que l'attribut `value` de l'élément change. L'évènement [`change`](/fr/docs/Web/API/HTMLElement/change_event) est différent, car il est uniquement déclenché lorsque la valeur est confirmée, que ce soit en appuyant sur la touche <kbd>Entrée</kbd> ou lorsqu'une option est choisie dans une liste. On notera que l'évènement `input` n'est pas déclenché lorsque du code JavaScript change la valeur d'un élément dans un script.

## Syntaxe

On utilisera le nom de l'évènement pour les méthodes [`addEventListener()`](/fr/docs/Web/API/EventTarget/addEventListener), ou on définira une propriété de gestion d'évènement.

```js
addEventListener("input", (event) => {});

oninput = (event) => {};
```

## Type d'évènement

`input` est un évènement [`InputEvent`](/fr/docs/Web/API/InputEvent) et hérite de [`UIEvent`](/fr/docs/Web/API/UIEvent).

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

Dans cet exemple, on affiche la valeur courante de l'élément [`<input>`](/fr/docs/Web/HTML/Element/input) lorsqu'elle est modifiée.

### HTML

```html
<input placeholder="Saisissez un texte quelconque" name="name" />
<p id="values"></p>
```

### JavaScript

```js
const input = document.querySelector("input");
const log = document.getElementById("values");

input.addEventListener("input", updateValue);

function updateValue(e) {
  log.textContent = e.target.value;
}
```

### Résultat

{{EmbedLiveSample("")}}

## Spécifications

{{Specifications}}

## Compatibilité des navigateurs

{{Compat}}

## Voir aussi

- [`beforeinput`](/fr/docs/Web/API/Element/beforeinput_event)
- [`change`](/fr/docs/Web/API/HTMLElement/change_event)
- [`invalid`](/fr/docs/Web/API/HTMLElement/invalid_event)
