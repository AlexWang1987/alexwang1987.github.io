# Web Foundations

Front-end has always been evolving. Maybe because there are lacking of sophisticated IDE(Integrated Development Environment).
The front pieces seems too loose. Unlike Java, which is standing on shoulders of eclipse IDE and becoming the most popular Oriented-Object language.

### how we build a web user interface?

Here is a typical working flow how we build a web user interface. In login.html file we construct our template:
```html
<button id='loginBtn'>Log In</button>
```
And then, It's time to put on "some clothes" for the button in theme.css and glue the css file on the main html:
```css
#loginBtn{
    border-radius:5px;
    background-color:#CCC;
}
```
Lastly, we use javascript to handle all the DOM manipulation ,event handlers, user interactions etc..
```javascript
    $('#loginBtn').click(function()
    {
        console.log('User is clicking the button');
    });
```

As we can see, All code are hardly reusable and working process seems too loose. As the project is getting more complex and complicated, All our code are falling into the hell.

Web components should be independable with specific purposes. and most importantly to be composable and highly reusable.

### What is a complete component?

Based on Object-Oriented designing. Here are basics building blocks a complete web component should have.

* **[Template]** which occupies a certain area for conveying intented meaning.
* **[Skin]** which is a crucial step when we want to customize its looking.
* **[Behaviors]** components may response to user interaction, like click, hover, mousedown, mouseup, summit, etc.
* **[Properties]** what attributes I have.
* **[State]** Web Component may have some changing states 
* **[Actions]** Web component can emit some specific actions for business purposes.



