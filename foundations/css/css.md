# CSS(Cascading Style Sheets)

## Core Concepts

#### What important role the CSS is playing at?

> CSS is a stylesheet language used to *skin* the presentation of the **Structured Elements** ( also known as **HTML** or **XML based** languages, such as SVG,XHTML) on various medias(paper ,speech, screen etc).

In a sentence:
> CSS adds **style attributes** to **tree-like nested components** in a **cascading way** on different **medias**.

### How many types of CSS Style Sheet Attributes?

In CSS world, There are infinite style attributes. you should think of every Skinning Target as a box. Style types are finite. The first one is:

* display (Box Generation)
    > Display maybe one of most important attributes, because it defines what mode the render will use. It will affect itself behavior and its children including its color, font, or layout maybe. **inline** and **block** are most commonly used, besides that, **grid**, **inline-block**,**flex**,**table** are also used often.
        
    * [none] (escaping rendering process)
        > The element is completely gone.
    * [Inline] ( a special visual mode)
        > The elements applied this mode can be comfortable with others siblings in the same line.

    * [block] CSS Box Model ( one of core modules of CSS)
        > You can think of every web component as a box. Its attributes used for visual formatting.
    * [flex] Flexible Box(another of core modules of CSS3)
        > you can think of it as better Box Model introduced in CSS3. best appropriate for different devices and screens. A flex container expands items to fill available free space or squeeze them to prevent overflow. and It's suit for components of applications.
    * grid, inline-block, inline-flex,list-item,table, etc. So, all skinning elements can be divided  into two categories: inline-level elements or block-level elements.

* position (how to position element, collaborating with left| top| right| bottom.);
    * static (in parental normal flow)
        >stand at **flow** position of its parent.
    * relative (jump out of normal flow position)     
        >set a offset related to its flow position.
    * absolute (jump out of normal flow position completely)
        > The parent don't need to allocate any space for it. the element position itself related to its closest positioned ancestor. 
    * fixed (jump out of normal flow position completely)
        > a similar positioning behavior comparing 'absolute' method, but its related to current window, without any effects when scrolling.
        > last positioning methods escape the normal flow, sometimes, it maybe cover other normal elements. Here,`z-index` can help to specify the z axis.

* float (jump out of normal flow position, stay at left or right side)
    > others elements could fill into the extra space as it can be. (if they want to start a new line to layout. `clear:both|left|right` will be helpful.

* margin 
    >( if there are no real content that exists in a block, margin collapsing may happen standing next to its siblings)
     
* border
* padding
* width / height / min/max width/height
    > represent only its content's dimension. if its content overflows `overflow=auto|scroll|hidden|visible` can help us constrict its visible behavior.
* visiblity
    > Its difference contrasting with `display=none` is that you can't see it, but it is there indeed, just white space.

* box-shadow
* font font-size/family/style/weight
* color[really should be call text-color]
    > red,green,blue.... #FFF #FFFFFF rgb(),rgba(),hls(),hlsa(),**transparent**
* opacity
    > to control the whole element's transparency.
* line-height [just for block-level elements]
* vertical-align [ just for inline-level elements]
* text-align [ just for inline-level elements]

### what it looks like of Tree-like nested things?
XML is naturally a tree structure.
```xml
<personalInfo>
    <name>AlexWang</name>
    <address>Beijing In China</address>
    <hobbies>
        <item>painting</item>
        <item>drawing</item>
        <item>fishing</item>
    </hobbies>
</personalInfo>
```
```html
<html>
    <head></head>
    <body></body>
</html>
```
```JSON
{
    "persons":[
        {
            name:'alex01',
            passwd:'xxxx'
        },
        {
            name:'alex01',
            passwd:'xxxx'
        },
    }
}
```
They are all tree-base structures roughly. In CSS world, all children can inherit style attributes from its ancestors. But in web component building process, we sometimes don't want our components to be changable or influenced by other styles. We should follow **Namespace Naming** conventions. I'll talk more details about it in my latter articles.

### What is exactly cascading way?
Cascading is a foundation feature of CSS, It's just a algorithm used to determine the final style attributes of a specific element from many **style sources**.

Sytle sources:

* Browser inherent default styles.
    > At early age of web, Different browsers have their unique some styles. which causes an unpredictable visual results in custom's browser. But it's getting better nowadays.
* Users preferences.(chrome settings or firefox users font-size etc..)
* Author styles which are linked to html

The priority is creasing. Author styles attributes can override its other sources. But if user-agent uses **!important** to lock the attributes, Author style still can not get its way. So, be careful when using **!important**.


### How many medias we many bump into?

#### MediaTypes

* **all** means the styles are appropriate for all devices.
* **screen** intended for computer screens.
* **print** these styles may be used for printing.
* **...** other output devices type.

#### Media Conditional Expression (Evaluated to be false or true)
* width
* height
* aspect-ratio
* .... [many more](http://dev.w3.org/csswg/mediaqueries/#mq-features)

There are some logical operators: and ,(or) not 
```css
@media (min-width: 640px) and (orientation: landscape) { ... }
@media speech and (min-width: 960px) and (orientation: landscape) { ...  }
@media (min-width: 960px), projection and (orientation: landscape) { ... }
@media not all and (adobetv) { ... } /*except adobetv*/
```

#### MediaQuery = MediaType + some Media Conditional Express

Which controls when styles to be applied. When these conditional expression are matched, the website's skin can automatically changed with same content.
[MediaQueries](http://dev.w3.org/csswg/mediaqueries). Here some usages:

```html
<link rel="stylesheet" media="(max-width: 960px)" href="800 optimized.css" />
```

```css
<style>
    @media (orientation: portrait) and (max-width: 640px) 
    {
      selectors...
    }
</style>
```

#### How to reuse our style sheets?

* *@import url list_media_queries*
```
@import url("print.css") print;//used in printing.
@import url("tv.css") projection, tv;//used in projection or tv
@import 'global.css';//used all media types
@import "common.css" screen, projection;
@import url('portrait.css') screen and (orientation:portrait);
```
and som other important At-rules

* @charset "GBK";//to indicate current stylesheet's encoding.
* @font-face{font-family: "familyID"; src:url("external font url.woff")} // to load external font resources.
* @keframes identifier {} // authoring keyframe style animation.
* @support expression
* etc..

All kinds of At-rule are using to extend CSS's functionalities for this multi-devices and complex using environment.

Now, we are now at most important part: 

###Skining(Styling)
* Passive
    > What is passive or active stylesheets applying. For example,`<button class='button border-radius theme-primary'> </button>`, this is typical passive approach, the benefit is that we can specify what styles can be applied clearly and not easily be influenced. which is essential way for modern web component styling.
* Active
    > The active method is like `Button{font-size:18px;background-color:red}`, which means all the Button in this document may all be effected in cascading way. It's too general and very hard to debug and track.

So, to make styles more reusable and composable, we have to reconstruct our style infrastructures in **Component-oriented Styling Designing** methods.

Here's a xml-like element:`<element id class style attributes></element>`

#### Basic Selectors
* Universal Selector *(asterisk) matches any element. So, 
```css
*.warning == .warning 
*#siderbar === #siderbar
namespace|* all element in namespace domain.
*|* all elements
|* all elements without any domain constraicton
```

* Element Selector
```
It's too general and aggressive, it would be better to use it for more global theme or like.
```
* ID Selector
```
ID selector is only used for a specific element, which is hard too reuse it. It's a good practice not use it in large project with may styles. 
```
* Attributes Selector
```css
CSS is so powerful, you can use it filtering any elements you want basing on their attribute-existing and their 
value-regx(^ $ * ~ | i/g/m.
```
* Class Selector
```
you can think of it as a *special attribute selector* aimed at class attribute. .classname === [class~=classname] 
```
and selectors can be nested to consist of more complex selectors. 
#### Combined Selectors
Adjacent selector (next-sibling selector)
`span + input{}` span's adjacent sibling
`span ~ input{}` span's next sibling
`span > input{}` span's direct chidren.
`span   input{}` span's descentdants
[more details documentation](https://drafts.csswg.org/selectors-3/#general-sibling-combinators)
#### Pseudo-class
Psedu-class is muck like media querying, the styles only be actived when the pseodu-class could be satisfied. That is to say, the styles much have some conditions

    ```css
    div.menu li ul {
      display: none;
    }
    
    div.menu li:hover > ul {
      display: block;
    }
    ```

#### Pseudo-elements
* ::after 
>::after pseudo-element matches a virtual last child of the selected element. It is typically used to add cosmetic content to an element by using the content CSS property. 
{content: attr(data-descr)} or {content: 'add last text child'}
* ::before
* ::first-line
* ::selection

So, a valid selector could be combined:

```[ns|][element][.classname | #id | [attributes][:psudoclass][::psudoelement] {}```

[Complete Selector Specification](A complete list of selectors in the Selectors Level 3 specification.)

### Style Units
There is measure there is unit. Units makes numbers meaningful.
#### Relative length units
Font-relative lengths | Viewport-percentage lengths 
#### Absolute length units (Absolute length units represents a physical measurement)
like px(Relative to the viewing device,screen=1 device pixel , printer= 1/96 in), mm, cm(10mm), in(2.54cm),pt(1/72in),pc(12pt)


