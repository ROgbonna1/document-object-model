# Document Object Model
![The Document Object Model](https://www.w3schools.com/js/pic_htmltree.gif)

* Tree of nodes/elements created by the browser
* JavaScript can be used to read/write/manipulate to the DOM
* Object Oriented Representation, meaning nodes have object properties and methods.

## The Document Object
* The `document` object has a number of properties and methods.
* `document.all` returns an array object that holds all elements of the document object. Array elements are indexed so they can be referenced by index number.
  For example: 
  * `document.all[0]` will return the `html` object.
  * `document.length` will return the number of nodes/elements.
  * `document.head` returns the `head` of the document
  * `document.body` returns the body
  * Other properties include `document.domain`, `document.domain`, `document.URL` and many more.

* Can use the `document` object to select elements. (e.g. `document.forms` will return an indexed collection of all forms in the document.)

### DOM Selectors
* Two types of selectors: _single element selectors_, _multiple element selectors_

* **Single Element Selectors**
  * `document.getElementById('id-name')` returns the first element object with ID `id-name`.
    * Can then use this to change styling and content. For Example:
      ```
        test = document.getElementById('test');
        test.style.background = '#0b0755';
        test.style.color = '#fff';
        test.textContent = 'This is a test';
        test.innerHTML = '<h1>We Love Test!</h1>';
      ```
  * `document.querySelector('query')` returns the first element that match the CSS Query Selector, `query`.
    For Example:
      * `document.querySelector('.test-class')` returns the first element with `class='test-class'`
      * `document.querySelector('#test-id')` returns the first element with `id='test-id'`
      * `document.querySelector('footer p')` returns the first paragraph element that is a child of a footer.
      * `document.querySelector('li:last-child')` returns the first `li` element that is the last element amongst its siblings.

* **Multiple Element Selectors**
  * `document.getElementsByClassName('class-name')` returns and indexed collection (an 'HTML Collection'). It is array-_like_ but not an array. Can be converted to one.
  * These methods can be called on any collection of nodes.
    For Example:
   ```javascript
   let list = document.querySelector('ul');
   let links = list.getElementsByClassName('list-items');
   ```
  * `document.getElementsByTagName('tag-name')`
    Example:
    ```javascript
    let lis = document.getElementsByTagName('li');
    for (let i = 0; i < lis.length; i ++) {
      console.log(lis[i]);
    } 
    ```
  * `document.querySelectorAll('query')` returns a **_node list_**. Node lists not only count elements but text nodes. Also, array methods can be called on node lists.

### Traversing the DOM
  * `Node.childNodes` returns all child nodes for a given node. Be careful: This includes text nodes.
  * `element.children` will return an HTMLCollection of only children _elements_.

> ** Note on HTMLCollection vs. NodeLists
>
> HTMLCollections are array-like but cannot use array methods. getElementsBy... methods return HTMLCollections
> NodeLists are array-like but can use `forEach()` as an iterator.
> `Node.childNodes` and `document.querySelectorAll()` returns a NodeList
> HTMLCollections are always _live_ meaning changes in the DOM automatically update the collection.
> NodeLists are live for `Node.childNodes` but static for `document.querySelectorAll()`.

  * `Node.firstChild` returns first child node.
  * `element.firstElementChild` returns first child element.
  * `Node.lastChild` and `element.lastElementChild` work as expected.

  * Can fetch parent node and parent element with `node.parentNode` and `element.parentElement`.
  * Can fetch sibling node and sibling element with `node.nextSibling` and `element.nextElementSibling`.
  * Can fetch previous siblings with `node.previousSibling` and `element.previousElementSibling.`

### Creating and Inserting Elements
* We can create and append element nodes easily with JavaScript
  ```javascript
  // Create element
  const li  = document.createElement('li');

  // Add class
  li.className = 'collection-item';

  // Add id
  li.id = 'new-item';

  // Add attribute
  li.setAttribute('title', 'New Item');

  // Create text node and append
  li.appendChild(document.createTextNode('Hello World'));
  ```  
### Removing and Replacing Elements
* We can replace and remove elements using `element.replaceChild(new, old)`, `element.remove()`, and `parent.removeChild(element)`.
```javascript
// REPLACE ELEMENT

// Create Element
const newHeading = document.createElement('h2');
// Add id
newHeading.id = 'task-title';
// New text node
newHeading.appendChild(document.createTextNode('Task List'));

// Get the old heading
const oldHeading = document.getElementById('task-title');
//Parent
const cardAction = document.querySelector('.card-action');

// Replace
cardAction.replaceChild(newHeading, oldHeading);

// REMOVE ELEMENT
const lis = document.querySelectorAll('li');
const list = document.querySelector('ul');

// Remove list item
lis[0].remove();

// Remove child element
list.removeChild(lis[3]);
```
* Can fetch, add, modify, and delete **Classes** and **Attributes**
```javascript
// Classes
const firstLi = document.querySelector('li:first-child');
const link = firstLi.children[0];

link.className;
link.classList;
link.classList[0];
link.classList.add('test');
link.classList.remove('test');

// Attributes
link.getAttribute('href');
link.setAttribute('href', 'http://google.com');
link.setAttribute('title', 'Google');
link.hasAttribute('title');
link.removeAttribute('title');
```

### Event Listeners
* We can call the `.addEventListener()` method on an element. This method takes two arguments: an event and a callback function that executes on the event.
  Example:
  ```javascript
  let btn = document.querySelector('.btn');
  btn.addEventListener('dblclick', highlightGreen);

  function highlightGreen(event) {
    console.log(`EVENT: ${event.type}`);
    btn.style.background = 'green';
  }
  ```
* Note: Events are objects with a number of properties and methods. One such property is `event.type` that returns the event type.
* Also Note: The callback function argument for the `addEventListener` method is passed an `event` object upon execution.

* **Mouse Event**: A few...
  * 'click'
  * 'dblclik'
  * 'mousedown'
  * 'mouseup'
  * 'mouseenter'
  * 'mouseleave'
  * 'mousemove'
* **Key Events**: A few...
  * 'keydown'
  * 'keyup'
  * 'keypress'
  * 'focus'
  * 'blur'
  * 'cut'
  * 'copy'
  * 'paste'
  * 'input'
  * 'change' (for `select` lists)

### Event Bubbling
* When an event fires on a node, that event bubbles up through all parent nodes. For example, when an `a` tag is clicked inside of an `li`, the `li` experiences that event and so does the surrounding `ul`, etc.

### Event Delegation
* We listen for when an event fires on a parent node and we delegate which child node is affected.
  For Example:
  ```
  document.body.addEventListener('click', deleteItem);

  function deleteItem(e){
    if(e.target.className === 'delete-item secondary-content') {
     console.log('delete item');
    }
  }
```

### Local & Session Storage
* `localStorage` is similar to `sessionStorage`, except that while data stored in `localStorage` has no expiration time, data stored in `sessionStorage` gets cleared when the page session ends — that is, when the page is closed.
* `localStorage` and `sessionStorage` are a part of the browser. The `window` object has `localStorage` and `sessionStorage` properties that store key-value pairs.
* `localStorage` only stores strings. Must use `JSON.stringify` and `JSON.parse` to go from objects to strings.
* Can set, query, and delete from local storage. Can use `JSON.stringify` and `JSON.parse` to go from iterable objects to strings.
  Example code:
  ```javascript
  // set local storage item
// localStorage.setItem('name', 'John');
// localStorage.setItem('age', '30');

// set session storage item
// sessionStorage.setItem('name', 'Beth');

// remove from storage
// localStorage.removeItem('name');

// get from storage
// const name = localStorage.getItem('name');
// const age = localStorage.getItem('age');

// // clear local storage
// localStorage.clear();

// console.log(name, age);

document.querySelector('form').addEventListener('submit', function(e){
  const task = document.getElementById('task').value;

  let tasks;

  if(localStorage.getItem('tasks') === null) {
    tasks = [];
  } else {
    tasks = JSON.parse(localStorage.getItem('tasks'));
  }

  tasks.push(task);

  localStorage.setItem('tasks', JSON.stringify(tasks));

  alert('Task saved');

  e.preventDefault();
});

const tasks = JSON.parse(localStorage.getItem('tasks'));

tasks.forEach(function(task){
  console.log(task);
});
```
