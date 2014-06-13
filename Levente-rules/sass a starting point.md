#sass: Super Simple Stuff

	This guide will show you some super simple sass variables, imports, mixins and how to use them. After this guide you ought to be confident enough to google for any other sass issue.

##Variable

Variables in sass are a name preceded by a $. For instance the variable hello would look like so.

```sass
	$hello
```

But thats pretty useless without some sort of value attached to it. So lets go ahead and rename "hello" to "red" ad define it to be the color red.


```sass
	$red: #ff0000;

```

Brilliant, but now how do we use this in a class? Its simple - just replace whereever you use "#ff0000" with "$red". So this:

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

 This looks like more code in order to accomplish same thing - and you'd be right to think that. However lets say you have a site where you use #ff0000 a lot, instead of doing a find and replace across all your classes to change it to a darker red - you can just simply change the variable red to a darker hex value. 

 ##Nesting

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
