# HTML Style Guide


## Table of Contents

1. Validity
2. Indentation
3. Comments
4. Attributes
5. Semantics
6. Accessibility 

------------------------------------------------


## 1. Validity

All HTML pages should validate against the [W3C Validator](http://validator.w3.org/), shall be encoded in UTF-8 and carry the html5 doctype:
``` html
<!DOCTYPE html>
<meta charset="utf-8">
<title>© 2012 Jan Beck</title>
 ```

## 2. Indentation & Formatting

### Spaces & Tabs
Indentation is done by a tab that is 4 spaces wide. 4 spaces can be used instead of a tab.

### Block, Inline and Groups
Block elements create new lines. Inline elements don't.
Empty lines should be used to divide groups of elements when appropriate.  

``` html
<div class="post">

	<h1>Der Process</h1>
	<p>Jemand musste <b>Josef K.</b> verleumdet haben, denn <i>ohne</i> dass er etwas Böses getan hätte, wurde er eines Morgens verhaftet.</p>
	<p><a href="#more">weiterlesen</a></p>	
	
	<h2>Weitere wichtige Werke:</h2>
	<ul>
		<li>Beschreibung eines Kampfes, 1902-1910</li>
		<li>Das Urteil, 1912</li>
		<li>In der Strafkolonie, 1914</li>
		<li>Die Verwandlung, 1916</li>
	</ul>
	
</div><!-- /.post -->
 ```
 
### PHP in HTML

When mixing PHP and HTML together, indent PHP blocks to match the surrounding HTML code. Closing PHP blocks should match the same indentation level as the opening block. `endif;` and `endwhile;` are preferred over curly braces.

``` html
<?php if ( $attachments ) : ?>

	<ul class="images">

		<?php foreach ( $attachments as $attachment ) : ?>

			<li><?php echo $attachment; ?></li>

		<?php endforeach; ?>

	</ul><!-- /.images -->

<?php endif; ?>
 ```
Taken from http://developer.fellowshipone.com/patterns/code.php

## 3. Comments

Comments should explain code as needed, where possible.

Comments shall be used to help identify closing tags. A slash followed by a CSS-like list of classes and ID helps to avoid a chaotic heap of anonymous closing tags at the end of a document.

``` html
<div class="container">

	<div class="primary">
		[...]
	</div><!-- /.primary -->
	
	<div class="sidebar">
		
		<div class="widget" id="blogroll">
			[...]
		</div><!-- /.widget#blogroll -->
		
		<div class="widget" id="categories">
			[...]
		</div><!-- /.widget#categories -->
		
	</div><!-- /.sidebar -->
</div><!-- /.container -->
 ```

You must only use this kind of identified closing tags when it would otherwise produce more than 2 anonymous closing tags.


## 4. Attributes & Tags

### Quotes

Always use quotes around attributes. Prefer double quotes over single quotes. However use HTML5-Syntax for empty attributes.

``` html
<input type="text" name="city" disabled>
```

### type Attributes

Omit type attributes for stylesheets and scripts.

``` html
<link rel="stylesheet" href="css/main.css">
<script src="js/application.js"></script>
```

### Void elements

Use HTML5-Syntax for `<br>`, `<hr>`, `<link>`, `<img>` and [other void elements](http://www.w3.org/TR/html-markup/syntax.html#void-element).

## 5. Semantics

### IDs

IDs shall be used as a way to easily hook JavaScript actions to DOM-Elements or/and gain performance boosts when using native element query methods.

Consider the following markup:

``` html
<ul id="navigation">
	<li><a href="/home">Home</a></li>
	<li><a href="/about">About</a></li>
	<li><a href="/contact">Contact</a></li>
</ul>
```

We can use jQuery to attach a handler to all links in this menu in performant way:

``` javascript
$('#navigation').find('a').click(fn);
```

Furthermore classes should be used instead of IDs.

### Classes

Classnames shall always contain dashes instead of underscores or camelCase.

Use a modular aproach when naming your parts:

``` html
<div class="header">
	
	<form class="search" method="get" action="search.php">
		<label class="search-title" for="s">What are you looking for?</label>
		<input class="search-input" id="s" type="text" placeholder="Type your search term" />
		<button class="search-submit">
	</form>

</div>
```

CSS rules would target each element directly based on its class in a non-hierarchical way.

``` css

.search { /* ... */ }
.search-title { /* ... */ }
.search-input { /* ... */ }
.search-submit { /* ... */ }
```

Modules should work even in another context or with different tags:

``` html
<div class="footer">
	
	<form class="search" method="get" action="search.php">
		<h3 class="search-title">What are you looking for?</h3>
		<input class="search-input" id="s" type="text" placeholder="Type your search term" />
		<input class="search-submit" type="submit">
	</form>

</div>
```
``` css
.footer .search { /* overwrite styles based on location */ }
```

The example above uses a very simple module-name `search`. In a more realistic environment this might target more than one module of that name.
In this case use a descriptive name of each individual module and prefix its children elements.

``` html
<div class="sidebar">
	
	<form class="blogsearch" method="get" action="search.php">
		<h3 class="bs-title">What are you looking for?</h3>
		<input class="bs-input" id="s" type="text" placeholder="Type your search term" />
		<input class="bs-submit" type="submit">
	</form>

</div>
```

Avoid multiple unsemantic classes like this:

``` html
<ul class="clearfix grid grid-12 grid-borderless">
```

Instead use one semantic class and attach classes using a preprocessor.

``` html
<ul class="recent-articles">
```

``` css
.recent-articles { 
	.clearfix;
	.grid(12);
	.grid-borderless;
}
``` 

## 6. Accessibility 

Value human accessibility over machine validity or semantics. Machines can adapt, update and eventually become better over time; Humans need access to information with what they have now.

### Define Landmarks

``` html	
<h1 role="banner">Sitename</h1>

<form role="search" method="post" action="search.php">...</form>

<ul id="nav" role="navigation">
	...
</ul>

<div id="content" role="main">
				
	<div id="post" role="article">
		...
	</div>
	
	<p role="complementary">
		...
	</p>
	
</div>
```

### Forms

...
