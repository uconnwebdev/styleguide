#sass: Super Simple Stuff

This guide will show you some super simple sass variables, imports, mixins and how to use them. After this guide you ought to be confident enough to Google for any other sass issue.

Written by [Levente Nagy](https://github.com/freshwaterfish1)

##Variable

**Variables** in sass are a name preceded by a $. For instance the **variable** hello would look like so.

```sass
	$hello
```

But thats pretty useless without some sort of value attached to it. So lets go ahead and rename "hello" to "red" ad define it to be the color red.


```sass
	$red: #ff0000;

```

Brilliant, but now how do we use this in a class? Its simple - just replace wherever you use "#ff0000" with "$red". So this:

```sass
	.class {
	color: #ff0000;
	}
```

Would turn into this:

```sass
	$red: #ff0000;
	 
	.class {
	color: $red;
	}
```

And when compiled the css would look like this:

```css

	.class {
	color: #ff0000;
	}
```

 This looks like more code in order to accomplish same thing - and you'd be right to think that. However lets say you have a site where you use #ff0000 a lot, instead of doing a find and replace across all your classes to change it to a darker red - you can just simply change the **variable** red to a darker hex value.

 ##Nesting

 The next thing you'll need to know about sass is how **nesting** works. Assuming you know css, it is up to you - as the coder to keep all your nested elements near each other in the css. However with sass you can have sass do all the heavy lifting for you. Lets say you have your nav, and want to define three things in it. Instead of doing the following css:

 ```css
nav ul {
  margin: 0;
  padding: 0;
  list-style: none;
}

nav li {
  display: inline-block;
}

nav a {
  display: block;
  padding: 6px 12px;
  text-decoration: none;
}
```

You can save yourself the trouble of all that by simply **nesting** them under the nav tag. The sass would look like this:

 ```sass
nav {
  ul {
    margin: 0;
    padding: 0;
    list-style: none;
  }

  li { display: inline-block; }

  a {
    display: block;
    padding: 6px 12px;
    text-decoration: none;
  }
}
```

And of course the sass would compile to the following css:

 ```css
nav ul {
  margin: 0;
  padding: 0;
  list-style: none;
}

nav li {
  display: inline-block;
}

nav a {
  display: block;
  padding: 6px 12px;
  text-decoration: none;
}
```
##Partials

**Partials** are sass files that start with and underscore to denote that they are partial files that aren't to be compiled into css files. For instance the file name could look like so:

```
_partial.scss
```

**Partials** are used with Imports which we will talk about in the next section.


##Import

**Imports** let you combine sass files together so when you compile your sass into css you get only one master file instead of having to do multiple css requests. All you need to perform a **import** is a partial css that you will sew into the "normal" non partial css file. So if we'd like to **import** _partial.scss

 ```sass
// _partial.scss

html,
body,
ul,
ol {
   margin: 0;
  padding: 0;
}
```

into base.scss

 ```sass
/* base.scss */

body {
  font-size: 100% Helvetica, sans-serif;
  background-color: #efefef;
}
```

all we have to do is the following:

 ```sass
/* _partial.scss */

@import 'reset';

body {
  font-size: 100% Helvetica, sans-serif;
  background-color: #efefef;
}
```
Oh, sass is smart so you don't need to bother adding in the .sass extension on the partial file. It'll sort it out all by itself. Anyways the final css output looks like this:

```css
html, body, ul, ol {
  margin: 0;
  padding: 0;
}

body {
  background-color: #efefef;
  font-size: 100% Helvetica, sans-serif;
}
```

##Mixins

**Mixins** lets you make groups of CSS declarations that you can reuse throughout your site. Since its horrible to have to retype every vendor prefix for all the types of "border-radius". Instead lets make it a **mixin**, which is compromised of sass elements we have mentioned earlier in this document. First off lets tell sass we are making a mixin.

 ```sass
@mixin
```
Now lets go ahead and name it "border-radius", since we will be using this mixin to adjust the css border-radius element.

 ```sass
@mixin border-radius
```
And now lets add in a variable so we can actually control the border-radius: 

 ```sass
@mixin border-radius($radius) {
}
```
And then add in all the vendor prefixes:

 ```sass
@mixin border-radius($radius) {
  -webkit-border-radius: $radius;
     -moz-border-radius: $radius;
      -ms-border-radius: $radius;
          border-radius: $radius;
}
```

Now all we got to do is use it in a class. To do this use "@include" and replace $radius with a value for the "border-radius":

 ```sass
@mixin border-radius($radius) {
  -webkit-border-radius: $radius;
     -moz-border-radius: $radius;
      -ms-border-radius: $radius;
          border-radius: $radius;
}

.box { @include border-radius(10px); }
```

And this sass will compile out to the following css:
```css
.box {
  -webkit-border-radius: 10px;
  -moz-border-radius: 10px;
  -ms-border-radius: 10px;
  border-radius: 10px;
}
```
##Extend/Inheritance

"**@extend**" allows you to share share a set of CSS properties from one selector to another. Lets say you have a message box with the following css.

```css
.message {
  border: 1px solid #ccc;
  padding: 10px;
  color: #333;
}
```

Now lets add in some types of messages for instance success, error, and warning. But since we are using sass we can keep our code pretty simple, just using @extend followed by the css class you'd like to use. 

```sass
.message {
  border: 1px solid #ccc;
  padding: 10px;
  color: #333;
}

.success {
  @extend .message;
}

.error {
  @extend .message;
}

.warning {
  @extend .message;
}
```
From there we can just add in our modifications for each type of message:

```sass
.message {
  border: 1px solid #ccc;
  padding: 10px;
  color: #333;
}

.success {
  @extend .message;
  border-color: green;
}

.error {
  @extend .message;
  border-color: red;
}

.warning {
  @extend .message;
  border-color: yellow;
}
```
And as always our sass compiles into the following css:

```
.message, .success, .error, .warning {
  border: 1px solid #cccccc;
  padding: 10px;
  color: #333;
}

.success {
  border-color: green;
}

.error {
  border-color: red;
}

.warning {
  border-color: yellow;
}
```

---
###References

**sass-lang**
>[http://sass-lang.com/guide](Sass Basics)
