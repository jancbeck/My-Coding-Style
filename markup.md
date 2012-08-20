# HTML Style Guide


## Table of Contents

1. Validity
2. Indentation
3. Comments
4. Attributes
5. Semantics

------------------------------------------------


## 1. Validity

All HTML pages should validate against the [W3C Validator](http://validator.w3.org/), shall be encoded in UTF-8 and carry the html5 doctype:
``` shtml
<!DOCTYPE html>
<meta charset="utf-8">
 ```

## 2. Indentation

block elements deserve a new line.
Mixed PHP indentation

## 3. Comments

Comments should explain code as needed, where possible.

Comments shall be used to help associate closing tags with its opening tags. A slash followed by a CSS-like list of classes and ID helps to avoid a chaotic heap of anonymous closing tags at the end of a document.

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