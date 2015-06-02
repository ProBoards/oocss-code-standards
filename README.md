# OOCSS code standards

The purpose of this document is to provide guidelines for writing CSS. Code conventions are important for the long-term maintainability of code. Most of the time, developers are maintaining code, either their own or someone else’s. The goal is to have everyone’s code look the same, which allows any developer to easily work on another developer’s code.

We've used [Idiomatic CSS](https://github.com/necolas/idiomatic-css) and [stubbornella](https://github.com/stubbornella/oocss-code-standards) as a base from which to build.

### Class Names

Class names should use dashes.  When dealing with code that may interact with older templates, prefer to leave class names unchanged, to preserve backwards compatibility with older templates.

```css
/* Good - use dashes */
.this-is-good {}

/* Bad - don't use camel case */
.thisIsBad {}

/* Bad - don't use underscores */
.this_is_bad {}


```

### Indentation

Each indentation level is made up of four spaces. Do not use tabs. (Please set your editor to use four spaces)

```css
/* Good */
.proboards {
    color: #fff;
    background-color: #000;
}

/* Bad - all on one line */
.proboards {color: #fff; background-color: #000;}
```

Rules inside of `@media` must be indented an additional level.

```css
/* Good */
@media screen and (max-width:480px) {
   .proboards {
       color: green;
   }
}
```

### Brace Alignment

The opening brace should be on the same line as the last selector in the rule and should be preceded by a space. The closing brace should be on its own line after the last property and be indented to the same level as the line on which the opening brace is.

```css
/* Good */
.proboards {
    color: #fff;
}

/* Bad - closing brace is in the wrong place */
.proboards {
    color: #fff;
    }

/* Bad - opening brace missing space */
.proboards{
    color: #fff;
}
```

### Property Format

Each property must be on its own line and indented one level. There should be no space before the colon and one space after. All properties must end with a semicolon.

```css
/* Good */
.proboards {
    background-color: blue;
    color: red;
}

/* Bad - missing spaces after colons */
.proboards {
    background-color:blue;
    color:red;
}

/* Bad - missing last semicolon */
.proboards {
    background-color: blue;
    color:red
}
```

### Exceptions and slight deviations

Large blocks of single declarations can use a slightly different, single-line
format. In this case, a space should be included after the opening brace and
before the closing brace.

```css
.selector-1 { width: 10%; }
.selector-2 { width: 20%; }
.selector-3 { width: 30%; }
```

Long, comma-separated property values - such as collections of gradients or
shadows - can be arranged across multiple lines in an effort to improve
readability and produce more useful diffs. There are various formats that could
be used; one example is shown below.

```css
.selector {
    background-image:
        linear-gradient(#fff, #ccc),
        linear-gradient(#f3c, #4ec);
    box-shadow:
        1px 1px 1px #000,
        2px 2px 1px 1px #ccc inset;
}
```

### Using CSS Preprocessors

Keep nesting to 3 levels deep. 

```scss
/* Good */
.proboards {
    .inner {
      ...

        .title {
         ....

            .subtxt {
            ...

            }
        }
    }
}

/* Bad - more than 3 levels of nesting */
.proboards {
    .inner {
      ...

        .title {
         ....

            .subtxt {
                ...

                .element {
                    ...

                }
            }
        }
    }
}
```

Declare `:extend` followed by LESS mixins first in a declaration block.

```scss
/* Good */
.proboards {
    @extend .company;
    @include font-size(14);
    color: #555;
    font-size: 11px;
}

/* Bad */
.proboards {
    color: #555;
    @extend .company;
    font-size: 11px;
    @include font-size(14);
}
```

### Vendor-Prefixed Properties

When using vendor-prefixed properties, always use the standard property as well. The standard property must always come after all of the vendor-prefixed versions of the same property.

```css
.proboards {
    -moz-border-radius: 4px;
    -webkit-border-radius: 4px;
    border-radius: 4px;
}
```

If a vendor prefixed property is used, -moz, -webkit, -o, -ms vendor prefixes should also be used. Vendor-prefixed classes should align to the left with all other properties.

```css
/* Good */
-webkit-border-radius: 4px;
-moz-border-radius: 4px;
border-radius: 4px;

/* Bad - colons aligned */
-webkit-border-radius:4px;
   -moz-border-radius:4px;
        border-radius:4px;
```

Suffix property value pairs that apply only to a particular browser or class of browsers with a comment listing browsers affected.

```css
background: #fcfcfc; /* Old browsers */
background: -moz-linear-gradient(...); /* FF3.6+ */
background: -webkit-gradient(...); /* Chrome,Safari4+ */
background: -webkit-linear-gradient(...); /* Chrome10+,Safari5.1+ */
background: -o-linear-gradient(...); /* Opera 11.10+ */
background: -ms-linear-gradient(...); /* IE10+ */
background: linear-gradient(...); /* W3C */
```

Suffix fallback with “Old browsers” and standard property with “W3C”. Add a plus or minus to indicate that a property applies to all previous browsers by the same vendor or all future browsers by the same vendor.

### Using !important

Do not use !important on CSS properties. The only time this is allowed is with the permission of a manager or senior developer, and only after all other options have been exhausted.

```css
/* Good */
.proboards {
   color: red;
}

/* Bad - don't use !important */
.proboards {
   color: red !important;
}
```

### Font Sizing

All font sizes must be specified using rem only with a pixel fall back. Do not use percentages, ems or pixels alone. (http://snook.ca/archives/html_and_css/font-size-with-rem)

```css
/* Good */
.proboards {
   font-size: 14px; /* pixel fall back rule should come first */
   font-size: 1.4rem;
}

/* Bad - uses ems */
.proboards {
   font-size: 1.2em;
}

/* Bad - uses percentage */
.proboards {
   font-size: 86%;
}

/* Bad - uses pixel only */
.proboards {
   font-size: 14px;
}
```

### HEX value

When declaring HEX values, use lowercase and shorthand (where possible), do not use color names

```css
/* Good */
.proboards {
    color: #ccc;
}

/* Bad */
.proboards {
    color: #CCCCCC;
}
```

### String Literals

Strings should always use double quotes (never single quotes).

```css
/* Good */
.proboards:after {
    content: "proboards";
}

/* Bad - single quotes */
.proboards:after {
    content: 'proboards';
}
```

### Background Images and Other URLs

When using a url() value, always use quotes around the actual URL. 

```css
/* Good */
.proboards {
    background: url("img/logo.png");
}

/* Bad - missing quotes */
.proboards {
    background: url(img/logo.png);
}
```

### Attribute values in selectors

Use double quotes around attribute selectors.

```css
/* Good */
input[type="submit"] {
    ...
}

/* Bad - missing quotes */
input[type=submit] {
    ...
}

/* Bad - using single quote */
input[type='submit'] {
    ...
}
```


### Do not use units with zero values

Zero values do not require named units, omit the “px” or other unit.

```css
/* Good */
.proboards {
   margin: 0;
}

/* Bad - uses units */
.proboards {
   margin: 0px;
}
```

### Internet Explorer Hacks

Browser specific styles should not be in separate per-browser stylesheets. We prefer to keep all the CSS for a particular object in one place as it is more maintainable.  Classes like .ie8 are available, and are preferred over hacks.

```css
/* Good - uses valid CSS */
.proboards {
   margin: 0px;
}
.ie8 .proboards {
   margin: -1px;
}

/* Bad - Hacky */
.proboards {
   margin: 0;
   _margin: -1px;
}
```

### Selectors

Each selector should appear on its own line. The line should break immediately after the comma. Each selector should be aligned to the same left column.

```css 
/* Good */
button,
input.button {
   color: red;
}

/* Bad - selectors on one line */
button, input.button {
   color: red;
}
```

### Class Qualification

Do not over-qualify class name selectors with an element type unless you are specifying exceptions to the default styling of a particular class.

``` css
/* Good */
.buttonAsLink {}

/* Bad - element name should be omitted */
span.buttonAsLink {}

/* Good - element is providing exceptions */
.buttonAsLink {}
span.buttonAsLink {}
```

### Scoped styles

All selectors for a particular component start with the wrapper class name.

```css
/* Good */
.calloutButton {
   color: blue;
}
.calloutButton span {
   color: green;
}

/* Bad - second rule missing scope */
.calloutButton {
   color: blue;
}
span {
   color: green;
}
```

### JavaScript Dependence

All rules should be coded to expect JavaScript to be enabled. Rules that apply when JavaScript is disabled should be preceded by the noJS class.

```css
/* Good */
.noJS .calloutContent {
   display: block;
}

/* Bad - don't use .js */
.js .calloutContent{
   display: none;
}
```

### :hover and :focus

If :hover pseudo class is styled, :focus should also be styled for accessibility. Focus styles should never be removed.

```css
/* Good */
a:hover,
a:focus {
   color: green;
}

/* Bad - missing :focus */
a:hover {
   color: green;
}
```

### Avoid using IDs

Selectors should never use HTML element IDs. Always use classes for applying styles to specific areas of a page.

```css
/* Good */
.header {
   height: 100px;
}

/* Bad - using an ID */
#header {
   height: 100px;
}
```

### Width and height on components

No heights on anything that contains text. Components should be flexible and their widths should be controlled by grids.

```css
/* Good - no width specified */
.calloutContent {
    border: 1px solid #ccc;
    background: #fff;
}

/* Bad - dimension specified */
.calloutContent {
    width: 200px;
    height: 150px;
    border: 1px solid #ccc;
    background: #fff;
}
```

### Naming classes

When labelling elements within a component with a class, try to avoid generic classes like ``.inner``, ``.hd``, ``.bd``. Instead, prefix the class name with the name of the component. This is to avoid CSS getting overwritten when classes are too generic.

```css
/* Good */
.boxHd {
    background: #ccc;
}
.boxBd {
    background: #ccc;
}

/* Bad */
.box .hd {
    background: #ccc;
}
.box .bd  {
    background: #ccc;
}
```

However when extending a component and styling the inner elements, try to use the base component's inner elements' class name for styling, instead of extending the class names of the inner elements as well.

```css
/* Good */
.boxSimple .boxHd {
    background: #ccc;
}
.boxSimple .boxBd {
    background: #ccc;
}

/* Avoid this if possible */
.boxSimple .boxSimpleHd {
    background: #ccc;
}
```


### Comments

Well commented code is extremely important. Take time to describe components,
how they work, their limitations, and the way they are constructed. Don't leave
others in the team guessing as to the purpose of uncommon or non-obvious
code.

Comment style should be simple and consistent within a single code base.

* Place comments on a new line above their subject.
* Keep line-length to a sensible maximum, e.g., 80 columns.
* Make liberal use of comments to break CSS code into discrete sections.
* Use "sentence case" comments and consistent text indentation.

Tip: configure your editor to provide you with shortcuts to output agreed-upon
comment patterns.

Example:

```css
/* ==========================================================================
   Section comment block
   ========================================================================== */

/* Sub-section comment block
   ========================================================================== */

/**
 * Short description using Doxygen-style comment format
 *
 * The first sentence of the long description starts here and continues on this
 * line for a while finally concluding here at the end of this paragraph.
 *
 * The long description is ideal for more detailed explanations and
 * documentation. It can include example HTML, URLs, or any other information
 * that is deemed necessary or useful.
 *
 * @tag This is a tag named 'tag'
 *
 * TODO: This is a todo statement that describes an atomic task to be completed
 *   at a later date. It wraps after 80 characters and following lines are
 *   indented by 2 spaces.
 */

/* Basic comment */
```
