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

**Spaces & Tabs**
Indentation is done by a tab that is 4 spaces wide. 4 spaces can be used instead of a tab.

**Block, Inline and Groups**
Block elements create new lines. Inline elements don't.
Empty lines should be used to divide groups of elements when appropriate.  

``` html
<div class="post">

	<h1>Kafka</h1>
	
	<p>Jemand musste <b>Josef K.</b> verleumdet haben, denn <i>ohne</i> dass er etwas Böses getan hätte, wurde er eines Morgens verhaftet.</p>
	<p><a href="#more">weiterlesen</a</p>	
	
	<ul>
		<li>Beschreibung eines Kampfes, 1902-1910</li>
		<li>Das Urteil, 1912</li>
		<li>In der Strafkolonie, 1914</li>
		<li>Die Verwandlung, 1916</li>
	</ul>
	
</div><!-- /.post -->
 ```
 
**PHP in HTML**
As with PHP, HTML indentation should always reflect logical structure. Use tabs and not spaces.

When mixing PHP and HTML together, indent PHP blocks to match the surrounding HTML code. Closing PHP blocks should match the same indentation level as the opening block. `endif;` and `endwhile;` are preferred over curly braces.

``` html
<?php if ( ! have_posts() ) : ?>
   <div id="post-1" class="post">
   
      <h1 class="entry-title">Not Found</h1>
      <div class="entry-content">
         <p>Apologies, but no results were found.</p>
         <?php get_search_form(); ?>
      </div>
      
    </div>
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

Leaving out script in JS refs is ok.
HTML5 style <br>, <link> and <meta>

## 5. Semantics


## 6. Accessibility 
