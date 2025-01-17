---
title: MutationRecord.previousSibling
slug: Web/API/MutationRecord/previousSibling
page-type: web-api-instance-property
tags:
  - previousSibling
  - MutationRecord
  - Property
  - Reference
browser-compat: api.MutationRecord.previousSibling
---

{{APIRef("DOM")}}

The {{domxref("MutationRecord")}} read-only property **`previousSibling`** is the previous sibling of an added or removed child node of the [`target`](/en-US/docs/Web/API/MutationRecord/target) of a {{domxref("MutationObserver")}}.

## Value

If a node is added to or removed from the [`target`](/en-US/docs/Web/API/MutationRecord/target) of a {{domxref("MutationObserver")}}, the value is the {{domxref("Node")}} that is the previous sibling of the added or removed node: that is, the node immediately before this one in the parent's {{domxref("Node.childNodes", "childNodes")}} list.

The value is `null` if there are no added or removed nodes, or if the node is the first child of its parent.

## Examples

### Log the previous sibling of a mutation

This adds a node every time you click the button. Then the observer logs the `textContent` of the `previousSibling` of the added node. The first time this is `null` because the target didn't have any children to begin with (so now it has only the most recently added node), but after this it logs the node after (the `previousSibling` of) the one we just added.

#### HTML

```html
<button id="add-nodes">Add a node</button>
<button id="reset">Reset</button>

<pre id="log" class="log">Previous sibling of added node:</pre>
<pre id="counter" class="log">Node count: 0</pre>
<div id="target"></div>
```

```css hidden
.log {
  border: 1px dotted black;
  padding: .5rem;
}
```

#### JavaScript

```js
const addNodes = document.querySelector("#add-nodes");
const reset = document.querySelector("#reset");
const counter = document.querySelector("#counter");
const target = document.querySelector("#target");
let nodeNumber = 1;

addNodes.addEventListener("click", () => {
  const newPara = document.createElement("p");
  newPara.textContent = `Node #${nodeNumber}`;
  nodeNumber++;
  target.appendChild(newPara);
});

reset.addEventListener("click", () => self.location.reload());

function logPreviousSibling(records) {
  for (const record of records) {
    if (record.type === "childList") {
      for (const newNode of record.addedNodes) {
        counter.textContent = `Node count: ${target.children.length}`;
        log.textContent = `Previous sibling of added node: ${newNode.previousSibling?.textContent}`;
      }
    }
  }
}

const observer = new MutationObserver(logPreviousSibling);
observer.observe(target, {childList: true});
```

#### Result

{{EmbedLiveSample("Log the previous sibling of a mutation", "", 250)}}

## Specifications

{{Specifications}}

## Browser compatibility

{{Compat}}
