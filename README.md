Syntatic.gs
===================

Welcome. This is a fork of Nosenation/Light-SCSS-Semantic.gs wich is another fork of **Semantic.gs**.

This is SCSS only Semantic.gs repo with CSS3 compliant updates. With prior changes cleverly made by [bhcarpenter](https://github.com/bhcarpenter).

About
-------------

No fuss about it. I made a fork of this project and named it **Syntatic.gs** because its still useful to me. Semantic.gs were for a good time a fair utility for structural layout. Unfortunately the lack of updates and addition of new CSS3 properties made it unsuitable for projects.

This fork is intended to adjust the code to my future projects. Feel free to use and I hope it helps.

----------

Using the grid
-------------------

Like Semantic.gs (https://github.com/tylertate/semantic.gs), Syntatic uses the same variables and mixins with very few differences. Let's review the basics:

## Getting started

 1. Include syntatic.gs scss file on your project;
 2.  Set your grid variables (column width, gutter width, and number of columns);
 3.  As in Semantic.gs, to use a fluid (percentage-based) grid rather than a fixed pixels, simply override one additional variable: `$total-width: 100%;`.


### Applying the grid

Again, as in Semantic.gs, the columns are defined from the mixins, so that the code below:
```sass
.article {
   @include column(9);
}
.section {
   @include column(3);
}
```
The following output will be displayed:
```css
.article {
	margin: 0px 1.04167%;
	width: 72.9167%;
}
.section {
	margin: 0px 1.04167%;
	width: 22.9167%;
}
```
As you see, some original entries have been removed (floats) to enhance the final code that is rendered with your own settings and rules (mixins or placeholder selectors).

So a better organization can be done here:

```sass
%float-left{
	float:left;
}
.article {
   @include column(9);
   @extend float-left;
}
.section {
   @include column(3);
   @extend float-left;
}
```
Resulting in sane code for your project:

```css
.article, .section {
	float: left;
}
.article {
	margin: 0px 1.04167%;
	width: 72.9167%;
}
.section {
	margin: 0px 1.04167%;
	width: 22.9167%;
}
```
### Nested columns
Following the same rules of Semantic.gs:
> A .row() mixin must be applied to the containing element of the nested
> columns. That mixin should contain the number of grid units of its
> parent (9, in this case), and the same number must be passed into the
> nested columns as a second parameter (.column(3,9) in the example
> below). Note that This is the most complicated feature of Semantic.gs,
> but nested columns in fluid layouts aren't generally supported by any
> other grid system, so one additional parameter is a small price to
> pay.
> *Semantic.gs oc. excerpt)*
>
>```sass
> article {
>   @include .column(9);
>
>   ul {
>      @include .row(9);
>
>      li {
>         @include .column(3,9);
>      }
>   }
>}
>```

### Push and Pull

The .push() and .pull() mixins allow you apply left and right indents to your columns. Those mixins weren't modified from original project:

```sass
.article {
   @include push(2);
}

// Compiled CSS (non fluid layout)
.article {
   margin-left: 170px;
}

.article {
   @include .pull(2);
}

// Compiled CSS (non fluid layout)
.article {
   margin-right: 170px;
}

```

---
## The Syntatic part

### Fluid and fluid only
This code  works exclusively with fluid values. The Web works best with fluid values. I think this is an issue that has already passed. Thanks to [bhcarpenter](https://github.com/bhcarpenter) columns and nested columns are ok.  

### Reducing the weight and remaining agnostic
GS's doesn't need to know from the outset whether it will use float left, right or inline block display. Some of the previously included statements might have been useful before, but are redundant after a dozen or more instances.

By removing them from the original code, normalizers and resets handle these details while keeping the code clean.

### Columns and *boxes*
Roughly, a **box** is a column minus margins and pads, for structural organization (Nope, It's not just a div). It's a layout support element, where the columns work to organize the content and the boxes are used to organize columns with or without media queries.

So when you want a box in your layout use the code below:

```sass
.article {
   @include column(9,$box:1);
}
```
This will create a box using the same grid calculations.

---
## Browser compatibility

Syntatic.gs supports modern browsers as well as Internet Explorer 8 and up.  
The sub-pixel rounding calculations have been totally removed from Syntatic.gs.
