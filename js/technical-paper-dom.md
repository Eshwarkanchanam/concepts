# Let's Understand DOM(Document Object Model)

## What is DOM?

- Programming interface for HTML
- A representation of HTML that can be accessed using Javascript
- When a web page is loaded, the browser creates the DOM for that specific page
- This allows for the creation of dynamic web pages where users can interact with the page

There are 6 main methods to search for nodes in DOM:

| Method                 | Searches by  | can call on element | Live? |
| :--------------------- | :----------: | :-----------------: | :---: |
| querySelector          | CSS-selector |         Yes         |   -   |
| querySelectorAll       | CSS-selector |         Yes         |   -   |
| getElementById         |      id      |          -          |   -   |
| getElementsByName      |     name     |          -          |  Yes  |
| getElementsByTagName   |  tag or `*`  |         Yes         |  Yes  |
| getElementsByClassName |    class     |         Yes         |  Yes  |

> [!NOTE]
> - There is `elem.matches(css)` to check if elem matches the given CSS selector.
> - There is `elem.closest(css)`to look for the nearest ancestor that matches the given CSS-selector. The elem itself is also checked.
> - `elemA.contains(elemB)` returns true if elemB is inside elemA (a descendant of elemA) or when `elemA==elemB`

## Modifying the document

### Creating an element

To create DOM nodes, there are two methods:

`document.createElement(tag)`

Creates a new element node with the given tag:

```
let div = document.createElement('div');
```

`document.createTextNode(text)`

Creates a new text node with the given text:

```let textNode = document.createTextNode('Here I am');```

### Insertion methods

- `node.prepend(...nodes or strings)` – insert nodes or strings at the beginning of `node`,
- `node.append(...nodes or strings)` – append nodes or strings at the end of `node`,
- `node.before(...nodes or strings)` –- insert nodes or strings before `node`,
- `node.after(...nodes or strings)` –- insert nodes or strings after `node`,
- `node.replaceWith(...nodes or strings)` –- replaces node with the given nodes or strings.

Arguments of these methods are an arbitrary list of DOM nodes to insert, or text strings (that become text nodes automatically).

Here’s an example of using these methods to add items to a list and the text before/after it:
```
<ol id="ol">
  <li>0</li>
  <li>1</li>
  <li>2</li>
</ol>

<script>
  ol.before('before'); // insert string "before" before <ol>
  ol.after('after'); // insert string "after" after <ol>

  let liFirst = document.createElement('li');
  liFirst.innerHTML = 'prepend';
  ol.prepend(liFirst); // insert liFirst at the beginning of <ol>

  let liLast = document.createElement('li');
  liLast.innerHTML = 'append';
  ol.append(liLast); // insert liLast at the end of <ol>
</script>
```

So the final list will be:
```
before
<ol id="ol">
  <li>prepend</li>
  <li>0</li>
  <li>1</li>
  <li>2</li>
  <li>append</li>
</ol>
after
```

There are also “old school” methods:

- `parent.appendChild(node)`
- `parent.insertBefore(node, nextSibling)`
- `parent.removeChild(node)`
- `parent.replaceChild(newElem, node)`

All these methods return node.

### Node removal

- To remove a node, there’s a method `node.remove()`.

> [!NOTE]
> if we want to move an element to another place – there’s no need to remove it from the old one.
> **All insertion methods automatically remove the node from the old place.**


## Reference links

- [https://javascript.info/modifying-document](https://javascript.info/modifying-document)