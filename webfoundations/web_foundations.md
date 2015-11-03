# Web Foundations

Front-end has always been evolving. Maybe because there are lacking of sophisticated IDE(Integrated Development Environment).
The front pieces seems too loose. Unlike Java, which is standing on shoulders of eclipse IDE and becoming the most popular Oriented-Object language.

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
Lastly, we use javascript to handle all the DOM manipulation ,event handlers, user interactions.

As we can see, All code are hardly reusable.

