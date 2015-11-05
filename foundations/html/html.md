# HTML(Hyper text Markup Language
HTML is only focusing on **information structure** and **sematics**. Here is a simple demo news:


*************
<h1>Alien Was Caught!</h1>
Big news, Just in this morning, A farmer found an alien in his backyard! The more exciting thing is that He caught it and put it into a cage.

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
It's well structured and more sematic.

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
    
```

There are tons of **Sematic Markups** [Complete W3.org Reference](http://www.w3.org/html/wg/drafts/)

