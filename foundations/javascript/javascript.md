# Javascript Core Concepts

As all we know, Front-end is getting more and more complex. Javascript is playing an important role in FE development. More news features have been added, the newest one is [ES6](http://exploringjs.com/es6/), and many proposals will be standardized in ES7. Javascript is extensively used in many areas, native,web,back-end, desktop development, etc. It all credits its simplicity and flexibility. Here I'll talk bout some deep contents.

## Function.

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

### **Functional Scope**.
Now, we know that a function is just a special object, it can be normally called and it has its attributes and behaviors. when It's invoked no matter which way, Firstly, **Functional Scope Object** is created. It's just a normal **hidden** object, all local varibles and functions are associalted to it. when this exceution is done(return), normally, this functional scope will be collected by garbage collector a little while later. **but** there is an exception, I'll talk about it latter. That's to say, when we invoke the function a function scope will be born(**Object Memory Allocation**) and it's recalled(**Object Memory Collection** when the function ends. It really makes sense from point of view of Memory Usage.
```
function peelApple(apple)
{
    //funtional scope created: {apple}
    
    //set local varible {apple,knife}
    var knife = true,
    
    //get scope varible
    console.log('peeling processing',apple);
    
    //local varible {apple,knife,done}
    var done = true
    
    //not local varible, what!!! what will happen? we probably know it will set at ancestors scope. why is that? see next topic.
    greate = true;
    
    return // functional scope will be destroyed by garbage collector normall, BUT!!!, there is an exception: Closure.
}
```

### Function Scope Chain

That is way may teacher told you: Using `var` to declare you varible or it'll be dropped to its ancestors traversely. And under the hood, **Function Scope Chain** works. here is a demo:
```
function serveApple()
{
    //functional scope: A = {washStepDone}
    var washStepDone = false;
    
    //A = {washStepDone,washApple}
    function washApple()
    {
        //functional scope: B = {} --chinTo--> A
        
        washStepDone = true;
        
        console.log('washStepdone');
    }
    
    //A = {washStepDone,washApple,sliceApple}
    function sliceApple()
    {
        //functional scope C = {} --chinaTo--> A
    }
    
    //A = {washStepDone,washApple,sliceApple,slideAppleDone}
    var slideAppleDown = false;
    
    //A = {washStepDone,washApple,sliceApple,slideAppleDone,serving}
    function serving()
    {
        //function scope D = {} --chinaTo-->A
        sliceApple();
    }
    
    
    washApple();
    
    if(washStepDone)
    {
        sliceApple();
        
        if(slideAppleDown)
        {
            serving();
        }
    }
}
```


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
