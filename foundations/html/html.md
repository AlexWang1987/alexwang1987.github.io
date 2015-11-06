# HTML(Hyper text Markup Language
HTML is only focusing on **information structure** and **sematics**. Here is a simple demo news:


*************
<h1>Alien Was Caught!</h1>
Big news, Just in this morning, A farmer found an alien in his backyard! The more exciting thing is that he caught it and put it into a cage.

Published by AlexWang in 21st Jan 2015 Beijing,China
*************

It's just a joke. The problem is how to markup the news appropriately.

``` html
<article>
    <h1>Alien Was Caught!</h1>
    <p>Big news, Just in this morning, A farmer found a alien in his backyard! The more exciting thing is that He caught it and put it into a cage.</p>
    <p>Published by AlexWang in 21st Jan 2015</p>
    <address>Beijing, China</address>
</article>
```
It's well structured and more semantic.

This is a dropdown 's skeleton:
```html
<DropdownButton>
    <Button>Age?</Button>
    <Menu>
        <MenuItem>5</MenuItem>
        <MenuItem>15</MenuItem>
        <MenuItem>25</MenuItem>
        <MenuItem>35</MenuItem>
    </Menu>
</DropdownButton>

<!--Here we define our own Elements-->
```

There are tons of **Sematic Markups** [Complete W3.org HTML5.1 Reference](http://www.w3.org/html/wg/drafts/).

## Block-level / Inline-level Element
The most common element is `<div>` which is generally used to divide our document into smaller block areas containing its own children.

Block-level elements will occupy a whole newline within parental flow and drive away others siblings. on the other hand, Inline-level ones are more conforming, aligned one by one from left to right.

## Global Attributes(basics)
* id
* title tooltip
* class
* style 
* hidden hidden elements when it is loaded.
* data- which used to exchange information between html and javascript
* tabindex
* onevents(onmouseover,onblur... all lower-cases)

```
<!--html data-definition-->
<element data-camel-cased-name/>

<!--javascript dom manipulation-->
element.dataset.camelCasedName 
```

Again, **Structure** and **Semantic**.

### DOM
Dom provides a way to manipulate these tree-nested object, such as search,add,lelete and so on. It's a glue layer providing a way that javascript can handle it.

### Webkit
Most popular **Layout** and **Rendering/Drawing** engine that is widely used in HTML/CSS.
