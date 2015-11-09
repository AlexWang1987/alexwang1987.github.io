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

```javascript
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
        
        sliceAppleDown = true;
        
        consle.log('sliceAppleDown');
    }
    
    //A = {washStepDone,washApple,sliceApple,slideAppleDone}
    var slideAppleDown = false;
    
    //A = {washStepDone,washApple,sliceApple,slideAppleDone,serving}
    function serving()
    {
        //function scope D = {} --chinaTo-->A
        
        console.log('serving process');
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
See, Functional Scope Chain is very clear, In my scope, If I don't have just ask for it from parent and continue to its global scope. Here is problem. if we do't use `var`, the global context will be wholly mess. In ES6 we have `let` and `const` keywords that help us declare our varible more accurately.

## Function Closure
Which is most powerful feature in Javascript and it's most difficult to grasp at the same time. Sometimes, it causes hug performance issue. I'll continue **Function Scope** topic and show some Closure features.
```javascript
function cooking (ingredients)
{
    //functional scope A;
    
    var pickupIngredients = function()
    {
        //functional scope B chain-to-> A
        console.log(ingredients);
    };
    
    return pickupIngredients;
}

var newReference = cooking([tamato,brocoli]);
```
* cooking function executes and returns a function(pickupIngredients);
* at last topic,I talked about scope chain. now `pickupIngredients` refer to its `scope A`. so, Even cooking is finished, it's scope object has not been collected. becuase its **reference counter** still lager than 0.
* the benefit is that we can preserve **execution context** and restore it at appropriate time. This is exactly the base requirement for **asychronious programming**. Simply speaking, we need to machanism to restore preview execution context after a asychronous callback.
* the bigest problem is memory leaking. if we attach closures to gloal object,`referece counter > 0` ,they will never be swiped out of memory.

In this demo `newReference` will set at 'window' object. Scope A never be released. Scope B can access its parental scope anytime. So, 'Asychonious Programming` is widely used in javascript engine, let's take more deeper.

## Javascript Engine (V8) Event Loop, Stack, Heap

V8 is a very polular engine which is heart for [Nodejs](www.nodejs.org) and [Chrome](https://www.google.com/chrome);
Here is a clear explanation [https://www.youtube.com/watch?v=8aGhZQkoFbQ],but I'll describe it simply.

### Stack
In javascript world, everything you can think is object, and all codes are organized in functions. So application is running by functions invoking functions and so on. which form a stack similar to Array. when a function is called, it is insert into the top of stack and executed, it can return removing out of the stack or invoke others function on and on. The number of functions of the stack is dynamic, what's the maximum, it's not constant, different js engine has different limitations, Here is my chrome in OSX 10.10 x64 `max call stack = 15565`, still pretty big.

### Heap.
As I discussed above, every function execution will be attached a function scope(execution enviroment), all local properties are throwed into heap, where varibles are created , consumed and collected quickly.

### Queue / Event Loop
In JS Engine, There are a event loop model, all function are driven by Event also known as `Event-Driven Programming`. All Events associated an function object line in the queue. When **stack** is empty, the first event in the queue gets invoked and until done. and next one, on and on. Here is an interesting demo:

```javascript
setTimeout(function myturn()
{
    console.log("It's my turn");
},2000);

//we understand that myturn will be invoked in 2s, but it is not guaranteed in extreme conditions. 2s latter, it may stand at last position of the queue. and wait to be called and executed.
```

Event loop model is never block, pretty proper for `concurrence` and `Event-Driven programming` in back-end environment. like `nodejs platform`.

## Bootstraped
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
One of benefits of **Script language** is that it does't need to precompile into machine code. It is all dynamic. There generally are two step: **Interpretation** and **Excecution**. The duty of interpretation is Object-Building process. when this javascript file is loaded it'll be evaled with **global scope**. First, **Original Code** then is interpreted. all internal functions will created recursively and include **local var declaration**, **executable code** can be actually executed at last step. Now, you will understand why we can not believe the execution order based on literal sequence:

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
## Global / GlobalContext

Simply Speaking, There just a tree in javascript engine. **global** is at top of it, also act as **top function scope**, all code are wrapped in it. because of **Function Scope Chain**, All Object mounted in the tree are accessible. It also easy influenced by `var` declaration.

In the Global Cotext, here are core objects and values, which are building blocks of javascript.
```javascript
function Global()
{
    //->Data types
    //Object Behaviors
}
```

// Value Existence
1. Not Existence
    > throw Error('Error type and detail messages')
2. Existence

    2.1 `undefined`: has only one value of `undefined`. Exist, but has never been initialized.
3. `object`: which is the most usefull data structure in may OOP languages like java, C++, etc. it's like a *hash map*, in javascript, its attributes can be added or deleted dynamically. here are some more dedicated purposes and specific objects.

    * `null`: You can think of it a special value of object. `Garbage collector` can collect those values safely.(carefully `typeof null //object` which is may be a bug). which has its many internal purposes.
    
    * `boolean`: which is very simple only and has only two values `true`,`false`.
    
    * `number`: You can believe that any value which can be a number or not number(`NaN`). if it's a number which can be divided into many concrete types. like `Infinity, -Infinity, `
    
    * `string`: which is one of most important data type in any languages. just a sequence of characters and it's immutable.
    
    * `function`: which is base block for organization of execution. As I've talked above, function object is a special object which is callable and has many other features.
    

## Object Prototype Chain
In essence, in any language designing, we need a machanism to reuse our code.
In javascript world all values of variables are object, but there are different ways to create them. Interestingly,Differenct objects from different origins share the same code. how does it happen `prototype`, we can consider it as `Sharing libaray`, For example.

``` javascript
var mynameFromliterals = 'alexwang'; // typeof myname == 'string'
var mynameFromNew = new String('alexwang'); // typeof myname == 'object',like array.

Object.getPrototypeOf(mynameFromliterals) === Object.getPrototypeOf(mynameFromNew) // true, see!, they are seem,but from different origins.

//These two objects we can use them normally, sometimes, we ignore evenly their differences. because they are all objects and share the behavior. they are identical from the prespective of application.
```
Here are some cases:
* var str = 'strvalue'; str can get sharing attributes from String.prototype
* var arr = []; arr can get sharing attribtes from Array.prototye;
* ....

In OOP world, objects are often created by `new` operator, and all objects inherite parental attributes from its `Class`, which has the same name of its constructor. which is a bit of confusing from freshes. all objects are not alone, they are all chained up to its top `Object.prototype`, so,`Object.getPrototypeOf(Object.prototype)
null`.
```javascript
    function Person()
    {
        this.name = 'alexwang';
        this.passwd = '******';
    }
    
    var person_01 = new Person();
    var person_02 = new Person();
    
    // prototype is where they share libaray codes.
    Person.prototype.shareMethod = function()
    {  
        console.log(this.name);
    }

    person_01.shareMethod();//alexwang
    person_02.shareMethod();//alexwang
```
So, all objects created by some constructor share same prototype, its location is at its constructor's prototype property. and It is fundamentally different from other OOP languages. of couse, we can use `Object.crate`to specify its prototype. which is very flexible.






