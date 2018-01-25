# CSS / SCSS Styleguide
## Table of Contents
1. [General](#general)
  - [Source](#source)
2. [CSS](#css)
  - [General principles](#general-principles)
  - [BEM and OOCSS methodology](#BEM-and-OOCSS-methodology)
  - [Whitespace](#whitespace)
  - [Line break](#line-break)
  - [Maintainability](#maintainability)
  - [Format](#format)
  - [Positioning choices](#positioning-choices)
  - [Z-index organization](#z-index-organization)
3. [SCSS](#scss)
  - [File organization](#file-organization)
  - [General principles](#general-principles)

## General
### Source
  - BEM: [css-tricks](https://css-tricks.com/bem-101/)
  - OOCSS: [OOCSS wiki](https://github.com/stubbornella/oocss/wiki)
  - SCSS comments: [sassdoc](http://sassdoc.com/)
  - Modernizr: [modernizr](https://modernizr.com/)
  - W3C Standards : [w3c](https://www.w3.org/standards/)

## CSS
### General Principles
  - Set block indent to 2 spaces
  - Sort properties alphabetically
  - Add semicolon after all declarations
  - Set color to lowercase and prefer shorthand hexadecimal
  - Remove units in zero-valued dimensions
  - Do not use !important properties
  - Use 0 to border instead of none

#### Bad
```css
.my-class {
  margin: 0px;
}

.my-class {
  border: none;
  width: 100%;
  display: block;
  color: #CCCCC;
}
```

#### Good
```css
.my-class {
  margin: 0;
}

.my-class {
  border: 0;
  color: #ccc;
  display: block;
  width: 100%;
}
```

### BEM and OOCSS methodology

##### BEM
The BEM (Block, Element, Modifier) methodology is a component-based approach to web development. The idea behind it is to divide the user interface into independent blocks :
- **Block** : standalone entity that is meaningful on its own.
- **Element** : a part of a block that has no standalone meaning and is semantically tied to its block.
- **Modifier** : a flag on a block or element. Use them to change appearance or behavior.

```css
/* CSS example */
.block {

}

.block--modifier {

}

.block__element {

}

.block__element--modifier {

}

/* SCSS example */
.block {
  &--modifier {

  }

  &__element {
    &--modifier {

    }
  }
}
```

#### OOCSS
The goal of OOCSS (Object Oriented CSS) is to find repeated visual patterns and to factorize them when possible.

##### Bad

```css
.box-1 {
  border: 1px solid #ccc;
  width: 200px;
  height: 200px;
  border-radius: 10px;
}

.box-2 {
  border: 1px solid #ccc;
  width: 120px;
  height: 120px;
  border-radius: 10px;
}
```

##### Good

```css
.box-1 {
  width: 200px;
  height: 200px;
}

.box-2 {
  width: 120px;
  height: 120px;
}

.box-border{
  border: 1px solid #CCC;
  border-radius: 10px;
}
```

#### Benefits of a combination of OOCSS and BEM
- **Modularity** : Block styles are never dependent on other elements on a page, so you will never experience problems from cascading.
- **Reusability** : Composing independent blocks in different ways, and reusing them intelligently, reduces the amount of CSS code that you will have to maintain.
- **Structure** : BEM and OOCSS methodology gives your CSS code a solid structure that remains simple and easy to understand.

### Whitespace
- Add a space before and after combinator
- Remove space before selector delimiter
- Add a space before opening brace
- Add a space after colon, remove before

#### Bad
```css
.my-class{
  background: #fff;
  color: #000;
}

.my-class> .my-class-b {
  background: #fff;
  color: #000;
}

.my-class , .my-class-b{
  background: #fff;
  color: #000;
}
```
#### Good
```css
.my-class {
  background: #fff;
  color: #000;
}

.my-class > .my-class-b {
  background: #fff;
  color: #000;
}

.my-class,
.my-class-b {
  background: #fff;
  color: #000;
}
```

### Line break
- Add a line break after opening brace
- Add a line break between declarations
- Add a line break after selector delimiter
- Add a line break before closing brace
- Add a blank line between css element

#### Bad
```css
.my-class{
  background: #fff; color: #000;
}
.my-class-b, .my-class-c {background: #fff; color: #000;}
```

#### Good
```css
.my-class-a {
  background: #fff;
  color: #000;
}

.my-clas-b,
.my-class-c {
  background: #000;
  color: #fff;
}
```


### Maintainability
- Do not use ID selectors
- Avoid general element selectors
- Keep your selectors short

#### Bad
```css
ul.nav li a.my-class {
  background: #fff;
  color: #000;
}
```


#### Good
```css
.my-class {
  background: #fff;
  color: #000;
}
```


### Format
- Prefer the shortest shorthand form possible for properties that support it
- Don't write trailing zeros for numeric values with a decimal point
- Don't write leading zeros for numeric values with a decimal point

#### Bad
```css
.my-class {
  margin: 1px 1px 1px 1px;
  padding: 2.0rem;
  opacity: 0.5;
}
```


#### Good
```css
.my-class {
  margin: 1px;
  padding: 2rem;
  opacity: .5;
}
```


### Positioning choices
To position elements, use properties preferably in this order :
1. display: block | inline | inline-block
2. display: table-cell
3. position: relative | absolute | fixed | sticky
4. float: left | right
5. display: flex

#### Notes

* Prefer positioning that will stick element to the natural page flow.
* The display-cell property is mainly used for vertical centering.
* The absolute positioning is a very powerful type of positioning : an element with this type of positioning is not affected by other elements and it doesn't affect other elements. An overuse or improper use can limit the flexibility of your site.
* As the flexbox specification is not yet finalized, not all browsers have implemented all features of Flexbox. That said, there is now good support across the board for flexbox.


### Z-index organization
* ```(0 - 99)``` : Elements and components

   For all html elements and website components including text, images, content blocks, drop down...
* ```(100 - 199)``` : Header and footer
* ```(200 - 299)``` : Special cases

   For special cases of elements that should be displayed above all other elements
* ```(300 - 399)``` : Modals
* ```(400 - 499)``` : Notifications

Choose your z-index range according to the type of element you want to position. However you can use the same z-index value for different elements inside the same range.


## SCSS
### File organization
```
sass
|--partials
|  |--base
|  |  |--_helpers.scss
|  |  |--_layout.scss
|  |  |--_...
|  |--template
|  |  |--_configs.scss
|  |  |--_images.scss
|  |--ui
|  |  |--_form.scss
|  |  |--_button.scss
|  |  |--_...
|  |--utils
|  |  |--_name.function.scss
|  |  |--_name.mixin.scss
|  |--vendors
|  |  |--_normalize.scss
|  |--_base.scss
|  |--_shame.scss
|--style-lte-ie8.scss
|--style-print.scss
|--style.scss
```

### File naming convention
* Functions : 'name-of-the-function' + '.function.scss' (one function by file)
* Mixins : 'name-of-the-mixin' + '.mixin.scss' (one mixin by file)

### General Principles
  - Do not nest selectors more than three levels
  - Never extend something that is already using an @extend
  - Adding out regular styles after the @extends and @includes allows us to properly override those properties, if needed.
