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

### what it looks like of Tree-like nested things?


### what is exactly cascading way?


### how many medias we many bump into?

