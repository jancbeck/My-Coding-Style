# CSS Style Guide


## Table of Contents

1. General Principles
2. Preprocessors
3. Validity
4. Comments
5. File Organization
6. Formatting 
	1. Selectors 
	2. Declarations
	3. Blocks
	4. Declaration order
7. Property & Value Notation
	1. Pixels vs. Ems vs. Percentage
8. CSS3

------------------------------------------------

## 2. Preprocessors

As of the writing of this document (Summer 2012) I'm using LESS on almost every project and because of it's very native feeling I don't really seperate CSS and LESS in my head so it won't be seperated in this document. 
LESS is a superset of CSS. Basic patterns when writing CSS (e.g. indenting properties) obviously also apply when creating a mixin with variables and guards in LESS but rules like nesting rules just don't apply when writing plain CSS.


## 3. Validity

While markup validity is important to provide future-friendly semantics for machines and accessibility for humans, website styling is a much more messy, less idealistic field. Invalid properties such as `zoom` or `DXImageTransform` are often necessary for basic support of older browsers while experimental vendor-prefixed properties like `-webkit-appearance` or `-moz-backface-visibility` won't let you pass [W3Cs CSS validator](http://jigsaw.w3.org/css-validator/) as well.
As a general rule of thumb use what ever is necessary to make your website look as well as possible for each of the browsers you targeted and provide basic support for the others. Do not rely on validators; test on as many devices as possible.


## 4. Comments

** Rever to Nicolas Gallaghers tips about writing comments:** https://github.com/necolas/idiomatic-css#3-comments

Well commented code is extremely important. Take time to describe components,
how they work, their limitations, and the way they are constructed. Don't leave
others in the team guessing as to the purpose of uncommon or non-obvious
code.

Comment style should be simple and consistent within a single code base.

* Place comments on a new line above their subject.
* Avoid end of line comments.
* Keep line-length to a sensible maximum, e.g., 80 columns.
* Make liberal use of comments to break CSS code into discrete sections.
* Use "sentence case" comments and consistent text indentation.

Tip: configure your editor to provide you with shortcuts to output agreed-upon
comment patterns.

#### Example:

```css
/* ==========================================================================
   Section comment block
   ========================================================================== */

/* Sub-section comment block
   ========================================================================== */

/**
 * Short description using Doxygen-style comment format
 *
 * Long description first sentence starts here and continues on this line for a
 * while finally concluding here at the end of this paragraph.
 *
 * The long description is ideal for more detailed explanations and
 * documentation. It can include example HTML, URLs, or any other information
 * that is deemed necessary or useful.
 *
 * @tag This is a tag named 'tag'
 *
 * @todo This is a todo statement that describes an atomic task to be completed
 *   at a later date. It wraps after 80 characters and following lines are
 *   indented by 2 spaces.
 */

/* Basic comment */
```


## 5. File Organization 

It often makes sense to split your project into multiple files. You should not use this as a mere convenience for avoiding large files though. It does not matter if a file contains 1000 lines or 10 lines of code as long as it's clear what's in it and what not. Avoid having more than 10 files in your directory. A person not familiar with your project should instinctively know where to look when he/she wants to change something.

Make use of the `@import` function of LESS that lets you split up your files into subparts that will be compiled into one single CSS file. When you aren't using LESS do not link to multiple files or use CSS native `@import` as it will slow down your sites loading and rendering process! 
Your project should be organized so it is most comfortable to work with for you and your co-workers. Let server-side tools handle file concatenation and minification for you.

A typical WordPress theme directory would look like this:

```
theme
├── css
│   ├── admin.css         // customize backend
│   ├── editor.css        // styles for WYSIWYG editor
│   └── style.css         // frontend styles
└── less
    ├── admin.less        // imports what's needed
    ├── editor.less       // imports what's needed
    ├── layout.less       // overall layout of frontend
    ├── mixins.less       // helpful mixins for CSS3 properties, clearfix etc.
    ├── normalize.less    // not a reset
    ├── print.less        // print-specific rules
    ├── style.less        // master import file
    ├── typography.less   // font settings, headings, lists…
    └── variables.less    // LESS vars
```
Note that the `css` directory remains untouched as it's just an output directory for the LESS compiler be it local or on the server. All changes happen in the `less` directory.

<!-- TODO: How would this look like for the goldilocks approach or responsive websites in general? -->

### Print Styles

Don't use a separate print.css file. Include your print styles inside your one main CSS file to save an extra HTTP-request like so:

```css

@media print { 

    * {
        background: transparent !important;
        color: #444 !important;
        text-shadow: none;
    }

    a,
    a:visited {
        color: #444 !important;
        text-decoration: underline;
    }

    img { page-break-inside: avoid }
    
    .header,
    .footer {
    	display: none;
    }
}
```

## 6. Formatting 

### Selectors

When grouping selectors use seperate lines for each rule. Make your selectors as short as possible and as long as necessary.

```css

h1,
#comments .author-link,
.header .nav a { 
	color: #333;
}
```

### Declarations

When grouping declarations use seperate lines for each declaration. Always end declarations with a semicolon. Put a space between property and value.
**Modifiers:** When there is only one selector *and* only one declaration inside a rule you may write it as a single line.

```css

.footer-nav {
	width: 100%;
	clear: both;
	background: #eee;
}
.hidden { display: none; }

```
