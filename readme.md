<!--
 _   _                                             
| | | |                                            
| | | |  _          ,         , _|_  _   _  _  _   
|/  |/  |/  /\/    / \_|   | / \_|  |/  / |/ |/ |  
|__/|__/|__/ /\_/   \/  \_/|/ \/ |_/|__/  |  |  |_/
|\                        /|                       
|/                        \|                       

-->
<style>
  h1:not(.ignore), h2:not(.ignore), h3:not(.ignore), h4:not(.ignore), h5:not(.ignore), h6:not(.ignore) {
    text-transform: capitalize;
  }
  .small {
    text-transform: lowercase;
  }
  .nowrap {
    white-space: nowrap;
    overflow: auto;
  }
</style>
<h1 class="ignore">What Is flex-system.css</h1>

flex-system.css is an easy to use, mobile first responsive grid system framework based on css [flex-box](https://developer.mozilla.org/en-US/docs/Learn/CSS/CSS_layout/Flexbox "Flexbox - Learn web development | MDN").
___
## Instalation
* ```bash
  npm install flex-system --save ;)
  ```
* ```html
  <link rel="stylesheet" href="cdn.flex-system.com">
  ```
* download [source files](https://flex-system.com/download-source) from [flex-system.com](https://flex-system.com)
## Usage
* `.container` class creates a container a wrapper around elements
 * `.container.on{$breakpoint}full-screen` takes the entire width of the screen.

 `$breakpoint` = \[`small-`, `medium-`, `large-`, `larger-`\]
 * `.container.sp-right-0` specifies that there is no white space on the right side of the
   `.container` class.
 * `.container.sp-left-0` does the same thing but in the left direction
   * the `.container.sp-{left/right}-0` works only from large screens and up.

Use `.flex-sys.container` to reduce conflict if you are using another css framework that uses the same name.
```html
  <section class="container">
    <!-- content -->
  </section>

  <!-- reducing conflict -->
  <section class="flex-sys container">
    <!-- flex-system container -->
  </section>
```
* The remainig space `100% of the screen width - .container width` is stored in the `.remaining` class
```html
<aside class="remaining">
  <nav>
    <!-- navigation -->
  </nav>
</aside>

<section class="container">
  <!-- main content -->
</section>
```
#### Flex Row Container
`.flex-row`, `.row-on{$breakpoint}`, `.row-reversed` are (main/row)-aixs parents, their children/flex-items flows in a **row** or **row reversed** direction
#### Flex Column Container
`.flex-column, .column-on{$breakpoint}, .column-reversed` creates a cross-axis parents, flex-items are stacked one after the the another or the opposite direction

The _**flex row**_ and _**flex column**_ classes are displayed as flex.

The `.inline-flex` class makes an element to be displayed as `inline-flex` container, it can be used width <q>flex row</q> containers and <q>flex column containers</q>
```html
  <div class="column-onsmall flex-row">
    <!-- onsmall stack on top of each other, but from medium and up stay in one row -->
  </div>
  
  <!-- inline-flex -->
  <div class="inline-flex row-reversed">
    <!-- flex in the inline direction and items are in a row but reversed from the normal flow of the document  -->
  </div>
```

In flex-system, flex items are defined to shrink if there is no space available, if you want to specify that flex items should not shrink use the `.no-shrink` class with a _**flex row**_ containers or _**flex column**_ containers.
```html
  <div class="flex-column no-shrink">
    <div class="half">half</div>
    <div class="half">half</div>
    <div class="half">half</div>
  </div>
```
## Wrapping behavior
`Flex Row Containers`  will wrap by default.

The `.nowrap` overwrites this behavior.

`.wrap-reversed` specifies that flex items will wrap in a reversed order.

The `.on{$breakpoint}-wrap` classes specifies that flex items will wrap within a breakpoint range.

The `.from-{$breakpoint}-wrap` classes specifies that flex items will wrap starting from a breakpoint.
```html
  <div class="flex-row onsmall-wrap nowrap">
    <!-- wrap onsmall only -->
  </div>
```
## Grid System Classes
Grid system classes specifies element dimentions inside a flex parent.

flex-system uses 12 columns grid system.
### Syntax
`$class-name`

Where `$class-name` is consist of a `prefix` and a `suffix`.

|Breakpoint Name|Breakpoint Range|Prefix|Suffix|
|--- |--- |--- |--- |
|Global|_not defined_|\[`slice` \| `fourth` \| `third` \| `half` \| `fill`\]|\[`1`, `2`, , , `5`, , `7` to `11`, \]|
|Medium|`>=600px`|`onmedium`|\[`1`, `2`, `fourth`, `third`, `5`, `half`, `7` to `11`, `fill`\]|
|Large|`>=992px`|`onlarge`|\[`1`, `2`, `fourth`, `third`, `5`, `half`, `7` to `11`, `fill`\]|
|Larger|`>=1200px`|`onlarger`|\[`1`, `2`, `fourth`, `third`, `5`, `half`, `7` to `11`, `fill`\]|

#### Example
```html
  <div class="fill onmedium-5 onlarge-third onlarger-half">
    <!-- fill onsmall and up, take 5 slices from medium and up, one third from large and up one half onlarger -->
  </div>
```
**Note:** the empty suffixes in the global breakpoint means that there is no `suffix` for this class. and it is written as `prefix` like `half`, `fill`, e.t.c.

The `"slice"` `prefix` is only used with \[`1`, `2`, `5`, `7` to `11`\] `suffixes`

`3`, `4`, `6` and `12` prefixes are replaced with `fourth`, `third`, `half`, `fill` respectivly.

## Spacing Classes
Spacing classes are "grid classes" - a number `$n`, which is \[`1`-`6`\], and they work within the specified range.
### Syntax
`$class-name-m$n`

#### Example
```html
  <div class="half-m1 onmedium-fill-m5 onlarge-8">
    <!-- onsmall only half - 1 (49%), onmedium only fill - 5 (95%) onlarge and up 8 slices -->
  </div>
```

### Taking The Available Space
`.{$breakpoint}available` class specifies that an element should takes the available space.

`.{$breakpoint}available-each` classes specifies that each direct element of a flex container should take the available amount of space.

`$breakpoint` = \[ , `onmedium-`, `onlarge-`, `onlarger-`\]

#### Example
```html
  <div class="row-reversed available-each">
    <!-- each direct element should take the available space -->
  </div>
  <div class="flex-row">
    <!-- (2 slices) ~ 16.666% -->
    <div class="slice-2"></div>
    <!-- the available space (10 slices) ~ 83.334% -->
    <div class="available"></div>
  </div>
```

### Element Order
`.{$breakpoint}order-$n` classes specifies element order inside the flex parent `$n` = \[`1`-`6`\].

`$breakpoint` = \[ , `onmedium-`, `onlarge-`, `onlarger-`\].
#### Example
```html
<div class="flex-column">
  <div class="fill order-3 onmedium-order-1">first onmedium and up, third onsmall</div>
  <div class="order-2">second</div>
  <!-- reducing conflict for global breakpoint only -->
  <div class="flex-sys order-1">first</div>
</div>
```
Use `.flex-sys.{$breakpoint}order-$n` classes to reduce conflict.
### Alignment On The Main Axis
The `.{$breakpoint}row-$direction` classes specifies flex items alignment within the flex parent in the main axis direction.

`$direction` = \[`start`, `end`, `center`\].

`start` is the default value. and it's used only from medium and up.

The `.space-$direction` or `.{$breakpoint}sp-$direction` classes are used to distribute available space in the main axis.

`$direction` = \[`between`, `around`, `evenly`\].
#### Example
```html
  <!-- alignment -->
  <div class="flex-row row-end onmedium-row-center onlarge-row-start">
    <div class="third-m5">item</div>
    <div class="third-m5">item</div>
    <div class="third-m5">item</div>
  </div>
  <!-- available space distribution -->
  <div class="flex-row space-between onmedium-sp-around">
    <div class="third-m5">flex-item</div>
    <div class="third-m5">flex-item</div>
    <div class="third-m5">flex-item</div>
  </div>
```
### Flex Lines Alignment
Flex lines alignment classes sets the distribution of space between and around content **items** along the cross-axis.

Flex lines alignment classes are the same as main axis alignment classes with some expectations.

* insteade of `row` prefix use the `line` prefix
* insteade of `space` prefix use the `line-sp-` prefix
* the line alignment classes contains the `stretch` value as in `.line-stretch`.
> the `start` value is used by default in flex-system, if you want the property's default value use the `.default` or `.line-stretch` classes.
#### Example
```html
  <!-- alignment -->
  <div class="flex-row line-end onlarge-line-center">
    <div class="available">flex-item</div>
    <div class="available">flex-item</div>
    <div class="available">flex-item</div>
  </div>
  <!-- space distribution -->
  <div class="flex-row line-sp-between onmedium-line-sp-around onlarge-line-stretch">
    <div class="available">flex-item</div>
    <div class="available">flex-item</div>
    <div class="available">flex-item</div>
  </div>
  <!-- using the default value which is stretch -->
  <div class="flex-row default">
    <div class="half" style="height: 150px">my height is 150px</div>
    <div>me too</div>
    <div>me too</div>
  </div>
```

### Aligment On The Cross Axis Classes For Flex Parent
The `.{$breakpoint}cross-$direction` classes are used to distribute space in the cross axis of a flex container.

`$direction` = \[`start`, `center`, `end`, `baseline`, `stretch`\]
> the `start` value is used by default in flex-system, if you want the property's default value use the `.default` or the `.stretch` classes.
#### Example
```html
  <div class="flex-row cross-end onmedium-stretch onlarge-cross-start">
    <div class="available onlarge-8">item</div>    
    <div class="half onlarge-4">item</div>    
  </div>
  <!-- the default value -->
  <div class="flex-row stretch space-between">
    <div class="third-m3">
      <img src="image.png" class="responsive">
    </div>
    <div class="third-m3">
      <img src="image.png" class="responsive cover">
    </div>
    ...
  </div>
```
### Aligment On The Cross Axis Classes For Flex Item
The `.{$breakpoint}self-$direction` classes specifies the distribution of the available space in the cross axis for a flex item.
`$direction` = \[`start`, `center`, `end`, `baseline`, `stretch`\].
#### Example
```html
  <div class="flex-row">
    <div class="available self-stretch">item #01</div>
    <div class="available self-end">item #02</div>
    <div class="available self-center">item #03</div>
  </div>
```
### Auto Margins
`.{$breakpoint}push-$direction`, `.{$breakpoint}-center-{x/y}` classes are used to push an element into a direction.

`$direction` = \[`top`, `right`, `bottom`, `left`\]
#### Example
```html
  <div class="flex-row">
    <div class="push-right onsmall-push-left">i will go right from medium and up</div>
    <div class="center-x onmedium-center-y">horizontally centered, vertically centered onmedium</div>
    <div class="onlarger-push-right"></div>
  </div>
```
### Display Toggling Classes
The `.none` class hides an element.
#### Display On Breakpoint Ranges
The `.display-{$breakpoint}` displays an element as flex within a breakpoint range.

If you want to display an element as block use the `.display-{$breakpoint}.as-block`.
#### Display Starting From A Breakpoint
To display an element starting from a breakpoint use the `.display-from-$breakpoint`.

If you want to display an element as block use the `.display-from-{$breakpoint}.as-block`.
#### Example
```html
  <div class="none display-onmedium">
    i'll be displayed as flex onmedium only
  </div>
  <div class="none display-from-large as-block">
    i'll be visible from large screens and up as block level element
  </div>
```
### Responsive Typography
flex-system.css supports responsive typograhy.
#### Headings
by default headings font-size is scalable when using flex system.
#### Examples
```html
<h1>respnsive typography</h1>

<!-- reducing conflict -->
<h1 class="flex-sys h1">respnsive typography</h1>
```
#### Responsive Paragraph
`.responsive` class makes a paragraph font-size responsive with the width of the screen.
```html
<p class="responsive">this is a responsive paragraph</p>
```
### Utility Classes
flex-system comes with some classes that can help you in a lot of situations.
#### Text alignment
`.{$breakpoint}text-{$direction}` classes aligns text and inline-level elements in the spacified direction

`$direction` = \[`start`, `end`, `left`, `right`, `center`, `justify`, `match-parent`\]
#### Example
```html
<div class="text-center">
  <img src="inline-element.png">
  <p>text</p>
</div>

<!-- to reduce conflict -->
<div class="flex-sys text-center onmedium-text-start">
  some text to be aligned...
</div>
```
it is very important to define the direction of the page if you want a cross browser support.
```html
<html lang="en" dir="ltr">
  <!-- if you are using a language that uses (rtl) direction you don't need to define the dir attribute you'll just define the lang attribute -->
  <div lang="ar">
   <p class="text-center onlarge-text-start"> 
     مرحبا أيها العالم
    </p>
  </div>
</html>
```
#### Helper Classes
`.full-width`, `.full-height`, `.full-width-height` classes specifies that an element should take full(width/height) or both of the containing element.

html and body elements will take the full height of the screen when using flex-system, if you dont want that to happen, give either of them a `.default` class.
```html
  <html>
    <body class="default">

    </body>
  </html>
```

`img.responsive`, `video.responsive` makes an image or a video element responsive

`img.cover`, `video.cover` specifies that the elements content would be croped to fit their sizes.

The element content will be resized to maintain its aspect ratio while filling the element's entire content box.

The `img.middle-vertically`, `video.middle-vertically` makes an image or a video to be centered vertically
#### reseting
flex system is adding some styles for some elements and they will be ignored if `.default` class is used

A <a href="#">link</a> `(anchor tag)` is styled by removing the <u><a href="#">underline</a></u> and the default color making it's color to be the color of it's containing element.

A list element (`ul`, `ol`), is styled by removing the default bullets or numbering, margin and padding.

Input elements are styled by removing the default outline and the user resizing ability.

The `.margin-0` or `m{t | r | b | l}-0`, `.padding-0` specifies that there is no margin or padding for the specified direction/directions.
```html
  <!-- one direction -->
  <h1 class="mt-0">margin top 0</h1>
  <!-- all directions -->
  <p class="margin-0">hello world</p>
```

The `.no-select`, `.no-drag` classes specifies that an element should not be selected like when you want to copy a text, or not to be draged.
```html
  <!-- no select -->
  <p class="no-select">you can't select and copy this text</p>
  <!-- no drag -->
  <img src="undraggable.png" class="no-drag">
```
The `.circle` class makes an element to appear like a circle.

`.sausage` or `.capsule` classes makes an element to appear like a capsule.
```html
  <!-- circle -->
  <img src="image.jpg" class="circle">
  <!-- .capsule or .sausage -->
  <button class="capsule">sausage button</button>
```
#### Text Formatting
|Class|Output|
|--- |--- |
|`.cap`|<span style="text-transform: capitalize;">flex system</span>|
|`.upper`|<span style="text-transform: uppercase">flex system</span>|
|`.lower`|<div style="text-transform: uppercase">upper case contains <span style="text-transform: lowercase">lower case</span> characters</div>|

`.text-nowrap` class suppresses line break (text wrapping).
<p class="nowrap">Lorem ipsum dolor sit amet consectetur, adipisicing elit. Suscipit explicabo itaque modi, quia rem numquam dolorum sed id optio tenetur recusandae consectetur temporibus sint, expedita animi nulla nemo magni quam!</p>

`.system-font` class makes an elements font to be like the devices system font.