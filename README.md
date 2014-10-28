Use Helper Classes to Dry and Scale Your CSS.
=================================

You are starting a large new web project looking around for a new CSS methodology that will help you scale your code. A growing set of techniques for writing modular CSS are out there including [SMACC](https://smacss.com/), [BEM](http://bem.info/), [OOCSS](http://oocss.org/). As you can see, lots and lots of techniques to write and organize CSS.

But is there anything that can help writing good CSS beside all theses tools that I can rely on to DRY and improve my code and reduce more repetitive CSS declarations for the most used properties like float, margin and padding. Helper classes (Utility classes) can help remove this repetition by creating a set of abstract classes that could be used over and over in HTML elements.

And because [Naming CSS Stuff Is Really Hard](http://seesparkbox.com/foundry/naming_css_stuff_is_really_hard), we will use these classes in HTML elements without creating new class names and rules for a specific new components.

Helper classes will be responsible for only doing one job and doing it well, doing this will make your code more reusable, scalable for many features that will be added in the future so whenever you want to create a new component you will combine some classes together to build it.

> â€œTreat code like Lego. Break code into the smallest little blocks
> possible.â€

> â€” [@csswizardry (via @stubbornella) #btconf](https://twitter.com/smashingmag/status/339024926197559296)

Let's see a simple example of what utility classes are and how we can use them, imagine the following snippet of code.

``` css
.left        { float: left; }
.right       { float: right; }

.text-left   { text-align: left; }
.text-right  { text-align: right; }
.text-center { text-align: center; }
```

We created a set of CSS rules that we can use later building new components. For example if you want to align some content to the left you can use `text-left` class and for other case use `left` or `right` classes to float elements.

Letâ€™s see another example of a box that needs to be on the left and center itâ€™s inner content.

We usually do something like this

``` html
<div class="box">
</div>
```

``` css
.box {
	float: left;
	text-align: center;
}
```

But we can achieve the same thing using some helper classes.

``` html
<div class="left text-center">
</div>
```

Notice how I removed the `box` class name and instead added some of our predefined classes `left` and `text-center`.

In case we want to change the float and align directions you can use another classes to do that.

``` html
<div class="right text-right">
</div>
```

Another good example you used before, that I consider an example of helper classes is the grid system, here is an example from [Foundation](http://foundation.zurb.com/docs/components/grid.html).

``` html
<div class="row">
	<div class="small-2 large-4 columns">...</div>
	<div class="small-4 large-4 columns">...</div>
	<div class="small-6 large-4 columns">...</div>
</div>
```

The framework provides a lot of classes that could be used and combined together to create a grid system with different width in different screen size, this flexibility can help create new customized layouts faster.

- `.small-2` and `.large-4` classes doing one thing that is to set the width of an element based on the screen size.

- The `.row` class set the width of the entire columns container.
- `.columns` class sets the padding and floats.

## Importance of Helper Classes
-  Can be applied and combined directly to any element at any context.

- Reduce the war of CSS specificity.

- Less CSS maintenance.

- Code and UI style consistency so everything will be measured and defined from the start to be consistent such as margin and padding.

- You can figure out whatâ€™s going on in HTML without thinking deeply about how the code is working, so from the first time you see the code it will make sense to you. `text-center` makes sense that it will center the text inside the element.

- Reusable code, we don't have to write new CSS every time you want to create a new component or a little design change as you saw in the previous box example.

- Reduce code repetition for properties like floats, display, margin and padding.

## Ways to Create Theses Classes in Your Project
- From the beginning of the project, if you have all the project designs this can be good for you to see the project from a high level and decide which colors, background, padding, margins and then create your classes.

- Defining the classes as you go, if the designs is ready or if you are designing in the browser. I think this way is better so you don't have to write all the classes in the beginning and you will encounter them during your implementation.

Lets see more examples categorized by CSS definitions which every project should have.

## Margin & Padding
I think margin and padding are the most used properties in our code, adding some abstract classes that can handle this huge use will DRY our CSS.

First start by defining a variable for the base space unit for your design, let's start with `1em` and on top of that you can create classes for different space sizes.

``` css
$base-space-unit: 1em;
```

``` css
// Top Margin
.margin-top-none        { margin-top: 0; }
.margin-top-quarter     { margin-top: $base-space-unit / 4; }
.margin-top-half        { margin-top: $base-space-unit / 2; }
.margin-top-one         { margin-top: $base-space-unit; }
.margin-top-two         { margin-top: $base-space-unit * 2; }

// Padding top
.padding-top-none        { padding-top: 0; }
.padding-top-quarter     { padding-top: $base-space-unit / 4; }
.padding-top-half        { padding-top: $base-space-unit / 2; }
.padding-top-one         { padding-top: $base-space-unit; }
.padding-top-two         { padding-top: $base-space-unit * 2; }
```

You also can choose a short class names to do the same purpose as the example below from [basscss](http://www.basscss.com/docs/utility/#white-space)

```css
.m0  { margin:        0 }
.mt0 { margin-top:    0 }
.mr0 { margin-right:  0 }
.mb0 { margin-bottom: 0 }
.ml0 { margin-left:   0 }
```

Choose what works for you and your team weather long or short names, the long names will make you HTML element more wider but it's more readable in contrast to the short names, sometimes you have to go to CSS code to figure out how it works.

## Width & Height
Imagine you want to set a section to be full height in different places of your website, the traditional way was some thing like this:

``` html
<div class="contact-section">
<!-- Some content goes here -->
</div>
```

``` css
.contact-section { full-height: 100%; }
```

and for other section you will do the same thing

``` html
<div class="services-section">
<!-- Some content goes here -->
</div>
```

``` css
.services-section { full-height: 100%; }
```

But we can reduce all of this with one class like `full-height`

``` html
<div class="full-height">
<!-- Some content goes here -->
</div>
```

Some examples including the `full-height` class we used above.

``` css
.fit              { max-width: 100%; }
.half-width       { width: 50% }
.full-width       { width: 100%; }
.full-height      { height: 100%; }
```

## Position & Z-index
The position classes could be combined by some other classes like z-index to create a complex layout, we also can create a set of classes to set the exact position where our element will be (right, left, right left, ..).

``` css
.fixed    { position: fixed; }
.relative { position: relative; }
.absolute { position: absolute; }
.static   { position: static; }
```

``` css
.zindex-1 { z-index: 1; }
.zindex-2 { z-index: 2; }
.zindex-3 { z-index: 3; }
```

``` css
.pin-top-right {
	top: 0;
	right: 0;
}

.pin-bottom-right {
	bottom: 0;
	right: 0;
}
```

The pin class names inspired by [Mapbox](https://www.mapbox.com/base/latest/base.css).

Let's extend the full-height example to contain an element positioned to the bottom right. [Demo](http://jsbin.com/matito/1/)

``` html
<div class="full-height relative">
	<div class="absolute pin-bottom-right padding-one">
		Text to bottom right
	</div>
</div>
```

By combining more than one class we can get the required result in less code. If you want to position the inner element on the top right you can use the `pin-top-right` instead of `pin-bottom-right` . You noticed in the above code we added a `padding-one` class so that we can make a padding space for the element and stay away from the screen edges.

## Float
Floating elements left or right can be done using `left` or `right` classes. `clearfix` can be used in the parent element to clear floats. [Demo](http://jsbin.com/cenuvo/1/)

``` css
.left  { float: left; }
.right { float: right; }

.clearfix {
	&:before,
	&:after {
		content: " ";
		display: table;
	}

	&:after { clear: both; }
}

```

## Align
Making text and content align to any direction.

``` css
.text-left      { text-align: left; }
.text-right     { text-align: right; }
.text-center    { text-align: center; }
.text-just      { text-align: justify; }

.align-top      { vertical-align: top;}
.align-bottom   { vertical-align: bottom;}
.align-middle   { vertical-align: middle;}
```

## Visibility Classes
Visibility classes are very important as it controllers how an element will hide or show depends on the screen size, devise orientation, touch screens or print. From my experience I found visibility classes are very important especially in responsive design.

``` css
.hide-on-small { display: none; }
.show-in-large { display: block; }
```

``` html
<div class="hide-on-small show-in-large">.hide-on-small .show-in-large</div>
```

The above element will be hidden on small screens and show on larger screens, notice that theses classes should be inside a media query so you can determine when small screen end and when larger screen start.

And also you can use it to control elements in touch devices.

``` css
.touch .show-for-touch { display: none; }
.touch .hide-for-touch { display: inherit; }
```

Notice in the example above the `.touch` class will be accessible in the HTML element when we add [Modernizr](http://modernizr.com/).

A very good example of visibility classes are [Foundation Visibility Classes](http://foundation.zurb.com/docs/components/visibility.html) and [Bootstrap responsive-utilities](http://getbootstrap.com/css/#responsive-utilities).

## Typography
In typography you can create classes for font weight and text manipulation like ellipsis text.

``` css
.bold     { font-weight: bold; }
.regular  { font-weight: normal; }
.italic   { font-style: italic; }

.ell {
	white-space: nowrap;
	overflow: hidden;
	text-overflow: ellipsis;
}

.break-word         { word-wrap: break-word; }
.no-wrap            { white-space: nowrap; }
```

## Colors
Now it comes to the surface of your design, every application has a different UI guides and brand rules which we can define in theses classes.

### Text Color
Which can be used to set different color schemes for different elements.

### Background Color
Which could be used to define background colors to different elements.

Lets see how this can be translated to code, first let's define our variables in SASS.

``` css
$white        :   #fff;
$gray         :   #2c3e50;
$dark-gray    :   #95a5a6;
$dark         :   #2c3e50;

$notice       :   #3498db;
$success      :   #1abc9c;
$alert        :   #e74c3c;
```

Second we can define our classes.

``` css
// Colors

.white            { color: $white; }
.gray             { color: $gray; }
.dark-gray        { color: $dark-gray; }

.notice           { color: $notice; }
.success          { color: $success; }
.alert            { color: $alert; }

// Background

.white-bg         { background-color: $white; }
.gray-bg          { background-color: $gray; }
.dark-gray-bg     { background-color: $darkgray; }

.notice-bg        { background-color: $notice; }
.success-bg       { background-color: $success; }
.alert-bg         { background-color: $alert; }
```

A very good and inspiring examples of using colors and background classes is the [Mapbox](https://www.mapbox.com/base/styling/color/) and the [Google Web Starter Kit](https://github.com/google/web-starter-kit/blob/master/app/styles/components/_helper.scss#L20).

![Mapbox colors styleguide](https://dl-web.dropbox.com/get/hosted/Screen%20Shot%202014-10-25%20at%2013.30.33.png?_subject_uid=1922450&w=AACrbkhEItk1wCYR-CJv5zU6-7I5N8e5gYfl5Lv58hmOKQ)

Another use case is the [notification component](http://jsbin.com/tigeqo/1/), let's see how we can style it with background classes.

``` html
<div class="white p1 mb1 notice-bg">Info</div>
<div class="white p1 mb1 success-bg">Success</div>
<div class="white p1 mb1 alert-bg">Alert</div>
```

[![Alerts](https://dl-web.dropbox.com/get/hosted/Screen%20Shot%202014-10-21%20at%2008.31.33.png?_subject_uid=1922450&w=AADcWdgYi4pWTK1U4UOVumOt2whBNKbsutllNL62KhocYg)](http://jsbin.com/tigeqo/1/)

## Lists
How many times you want to get ride of the bullets and padding from the `ul` element , [`list-bare`](https://github.com/inuitcss/objects.list-bare) class can do that for you this time.

``` css
.list-bare {
	padding: 0;
	list-style: none;
}
```

## Borders
Adding borders to an element whether for all sides or one side

```
$border-color: #f2f2f2;
```

``` css
.border-all      { border:         1px solid $border-color; }
.border-top      { border-top:     1px solid $border-color; }
.border-bottom   { border-bottom:  1px solid $border-color; }
.border-right    { border-right:   1px solid $border-color; }
.border-left     { border-left:    1px solid $border-color; }
```

## Display
Display also could be set the same way as following.

``` css
.inline       { display: inline; }
.block        { display: block; }
.inline-block { display: inline-block; }
.hide         { display: none; }
.flex         { display: flex; }
```

## Conclusion
Following this principle of abstraction might be different approach from what we are used to author CSS. But after I and [others](http://www.smashingmagazine.com/2013/10/21/challenging-css-best-practices-atomic-approach/) tried it I can say this a very good approach to consider on your next project.

You can check the complete classes on this post on a new library I created called [css-helpers](https://github.com/ahmadajmi/css-helpers).

#### Further Reading
- [Challenging CSS Best Practices](http://www.smashingmagazine.com/2013/10/21/challenging-css-best-practices-atomic-approach/) [Must Read]
- [ACSS: Rethinking CSS Best Practices](http://www.slideshare.net/renatoiwa/acss)
- [Mediumâ€™s CSS is actually pretty f***ing good](https://medium.com/@fat/mediums-css-is-actually-pretty-fucking-good-b8e2a6c78b06)

#### Code Examples

- Learn from and explore the structure of [Mapbox styleguide](https://www.mapbox.com/base/) - [base.css](https://www.mapbox.com/base/latest/base.css)
- [Basscss](http://www.basscss.com/)
- [Foundation utility classes](http://foundation.zurb.com/docs/utility-classes.html)
- [Bootstrap Helper classes](http://getbootstrap.com/css/#helper-classes)
- [uikit utility classes](http://getuikit.com/docs/utility.html)
