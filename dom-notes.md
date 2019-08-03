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
