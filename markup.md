# HTML Style Guide


## Table of Contents

1. General Principles
2. Validity
3. Indentation
	1. Spaces & Tabs 
	2. Block, Inline and Groups
	3. PHP in HTML
4. Comments
5. Attributes
	1. Quotes
	2. type Attributes
	3. Void Elements
	4. HTML5 Elements and Accessibility
6. Semantics
	1. IDs
	2. Classes

------------------------------------------------

## 0. General Principles

From all layers of progressive enhancement (markup, presentation, behavior) markup is probably the most overlooked yet it is often the one that is the hardest to change after its initial write-down. In the final production environment HTML might be be generated from multiple origins and dependencies are often unforseeable. Giving your HTML code a minute more of a thought can save you 10 minutes of fiddling with CSS and 1 hour of debugging JavaScript and/or IE.


## 1. Validity

All HTML pages should validate against the [W3C Validator](http://validator.w3.org/), shall be encoded in UTF-8 and carry the html5 doctype:
``` html
<!DOCTYPE html>
<meta charset="utf-8">
<title>Blog | © 2012 Jan Beck</title>
 ```

## 2. Indentation & Formatting

### Spaces & Tabs
Indentation is done by a tab that is 4 spaces wide. 4 spaces can be used instead of a tab.

### Block, Inline and Groups
Block elements create new lines. Inline elements do not create new lines.
Empty lines should be used to divide logical groups of elements when appropriate.  

``` html
<div class="post">

	<h1>Der Process</h1>
	<p>Jemand musste <b>Josef K.</b> verleumdet haben, denn <i>ohne</i> dass er etwas Böses getan hätte, wurde er eines Morgens verhaftet.</p>
	<p><a href="#more">weiterlesen</a></p>	
	
	<h2>Weitere wichtige Werke:</h2>
	<ul>
		<li>Beschreibung eines Kampfes, 1902-1910</li>
		<li>Das Urteil, 1912</li>
		<li><strong>In der Strafkolonie, 1914</strong></li>
		<li>Die Verwandlung, 1916</li>
	</ul>
	
</div><!-- /.post -->
 ```
 
### PHP in HTML

When mixing PHP and HTML together, indent PHP blocks to match the surrounding HTML code. Closing PHP blocks should match the same indentation level as the opening block. `endif;` and `endwhile;` are preferred over curly braces for better readability.

<!-- Taken from http://developer.fellowshipone.com/patterns/code.php -->

``` html
<?php if ( $attachments ) : ?>

	<ul class="images">

		<?php foreach ( $attachments as $attachment ) : ?>

			<li><?php echo $attachment; ?></li>

		<?php endforeach; ?>

	</ul><!-- /.images -->

<?php endif; ?>
 ```
 
When appropriate wrap each part of a template function into individual PHP-blocks instead of one big block so they can easily be moved around:

``` html
<div class="page">

	<?php get_header(); ?>
		
	<?php get_article(); ?>
	
	<?php get_sidebar(); ?>
	
	<?php get_footer(); ?>
	
</div>
 ```
 
## 3. Comments

Comments should explain code as needed, where necessary.

Comments shall be used to help identify closing tags. A slash followed by a CSS-like list of classes and/or IDs helps to avoid a chaotic heap of anonymous closing tags at the end of a document.

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

Always use quotes around attributes. Prefer double quotes over single quotes. Use HTML5-Syntax for empty attributes.

``` html
<input type="text" name="city" disabled>
```

### type Attributes

Omit type attributes for stylesheets and scripts.

``` html
<link rel="stylesheet" href="css/main.css">
<script src="js/application.js"></script>
```

### Void Elements

Use HTML5-Syntax for `<br>`, `<hr>`, `<link>`, `<img>` and [other void elements](http://www.w3.org/TR/html-markup/syntax.html#void-element).

### HTML5 Elements and Accessibility

Be aware of the fact that using the elements that HTML5 introduced currently do not help any machine or human better understand your site.
So when you write code like this

``` html	
<header>
	<!-- site name etc… -->
</header>

<section>
	<article>
		<!-- your main article content… -->
	</article>
	<aside>
		<nav>
			<!-- navigational elements… -->
		</nav>
		<form action="search.php">
			<!-- search form… -->
		</form>
	</aside>
</section>

<footer>
	<!-- footnotes… -->
</footer>
```

you are helping nobody but instead you might run into problems with older browsers and your markup depends on JavaScript for them to understand it. Elements like `header` and `footer` are not ment to be used just once on a first-level basis but to be used everywhere recursively nested down the document (E.g. `header` could be the part in a comment below an article that shows information about the author of the comment).

A better way would be to use WAI ARIA landmarks that will help screenreaders and parsing robots a lot and *already today*. 
Landmarks are ment to signalize individual parts of your document. That means you can much better use them to structure your document and even make your classes complement them for later CSS-Styling. 

``` html	
<div role="banner" class="banner">
	<!-- site name etc… -->
</div>

<div role="main" class="main">
	<div role="article" class="article">
		<!-- your main article content… -->
	</div>
	<div role="complementary" class="complementary">
		<ul role="navigation" class="navigation">
			<!-- navigational elements… -->
		</ul>
		<form role="search" class="search" action="search.php">
			<!-- search form… -->
		</form>
	</div>
</div>

<div role="contentinfo" class="contentinfo">
	<!-- footnotes… -->
</div>
```

## 5. Semantics

### IDs

IDs shall be used for anchor navigation, linking labels to form fields or as a way to easily hook JavaScript actions to DOM-Elements or/and gain performance boosts by using native element query methods.

Consider the following markup:

``` html
<ul id="navigation">
	<li><a href="/home">Home</a></li>
	<li><a href="/about">About</a></li>
	<li><a href="/contact">Contact</a></li>
</ul>
```

We can use jQuery to attach a handler to all links in this menu in a performant way using native browser select algorithms:

``` javascript
$('#navigation').find('a').click(fn); // uses document.getElementById() internally
```

Furthermore classes should be used instead of IDs because they can cause problems with specificity in CSS rules later.

### Classes

Class names shall always use dashes instead of underscores or camelCase to seperate words in them.

Use a modular aproach when naming your parts:

``` html
<div class="header">
	
	<form class="search" action="search.php">
		<label class="search-title" for="s">What are you looking for?</label>
		<input class="search-input" id="s" type="text" placeholder="Type your search term" />
		<button class="search-submit">
	</form>

</div>
```

CSS rules would target each element directly based on its class in a non-hierarchical way.

``` css

.search { /* ... */ }
.search-title { /* ... */ }
.search-input { /* ... */ }
.search-submit { /* ... */ }
```

Modules should work even in another context or with different tags:

``` html
<div class="footer">
	
	<form class="search" action="search.php">
		<h3 class="search-title">What are you looking for?</h3>
		<input class="search-input" id="s" type="text" placeholder="Type your search term" />
		<input class="search-submit" type="submit">
	</form>

</div>
```
``` css
.footer .search { /* overwrite styles based on location */ }
```

The example above uses the very simple module name `search`. In a more realistic environment this might target more than one module of that name.
In this case use a descriptive name of each individual module and prefix its children elements. This allows to refactor certain modules for multiple use cases.

``` html
<div class="sidebar">
	
	<form class="usersearch" action="usersearch.php">
		<h3 class="us-title">Who are you looking for?</h3>
		<input class="us-input" id="user" type="text" placeholder="User name to search for" />
		<input class="us-submit" type="submit">
	</form>

</div>
```

Avoid multiple unsemantic and purely presentational classes like these:

``` html
<ul class="clearfix grid grid-12 rounded">…</ul>
```

Instead use one semantic class and attach classes using a preprocessor.

``` html
<ul class="recent-articles">…</ul>
```

``` css
/* using LESS */
.recent-articles { 
	.clearfix();
	.grid(12);
	.border-radius(5px);
}
``` 

<!-- ### Forms -->
