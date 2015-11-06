# Javascript Core Concepts

As all we know, Front-end is getting more and more complex. Javascript is playing an important role in FE development. More news features have been added, the newest one is [ES6](http://exploringjs.com/es6/), and many proposals will be standardized in ES7. Javascript is extensively used in many areas, native,web,back-end, desktop development, etc. It all credits its simplicity and flexibility. Here I'll talk bout some deep contents.

## What is the Function.

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

### What is **Functional Scope**.



## How Javascript is getting constructed and bootstraped.
When A piece code of JS loaded into Javascript Engine, here is what happens.

```javascript
//Demo.js
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
One of benefits of **Script language** is that it does't need to precompile into machine code. It is all dynamic. There generally are two step: **Interpretation** and **Excecution**. The duty of interpretation is Object-Building process. when this javascript file is loaded it'll be evaled with **global scope**. and **magic** happens. First, **Original Code** then is interpred. all internal functions will created recursively and include **local var declaration**, **excecutable code** can be actually executed when it needs to be invoked. Now, you will understand why we can not believe the excecution order based on literal sequence:

```javascript

step1();
step2();
step3();

var msg = 'step3 is running';

function step3()
{
    console.log(msg);
}

function step2()
{
    console.log('step2');
}

function step1()
{
    console.log('step1');
}
```
