# Javascript Core Concepts

As all we know, Front-end is getting more and more complex. Javascript is playing an important role in FE development. More news features have been added, the newest one is [ES6](http://exploringjs.com/es6/), and many proposals will be standardized in ES7. Javascript is extensively used in many areas, native,web,back-end, desktop development, etc. It all credits its simplicity and flexibility. Here I'll talk bout some deep contents.

## What is the function in javascirpt.

The `function` in javascript is quite different from other stricted languages like java or c++. In essence, `function` in javascript is an `object` and can be `callable`, that's where `call` and `apply` comes in. we can also `invoke` it in traditional way using `()` expression.

```javascript
function bootstrap()
{
    console.log('It is bootstraping');
}

//Traditional Way.
bootstrap(param01);

//Object-Oriented Way
bootstrap.call(null,param01,param02);
//or
bootstrap.apply(null,[param01,param02]);
```

## How Javascript is getting constructed and bootstraped.
When A piece code of JS loaded into Javascript Engine, here is what happens.

```javascript
function composeEmail(name,city,country)
{
    var newMail = {
        name : name,
        city : city,
        country: country,
        date: new Date()
    };
    
    return newMail;
}

function sendEmail(email)
{
    console.log('Email is being sent',email);
    
    return 'done';
}

//Here we go.
var name = 'alexwang';
var city = 'beijing';
var country = 'China';

//write an email && send it.
var newEmail = composeEmail(name,city,country);
var result = sendEmail(newEmail);

console.log('Error or Done' + result);

```