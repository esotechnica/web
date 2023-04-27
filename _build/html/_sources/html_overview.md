# Overview

The current version of HTML (HTML5) is maintained by the [WHAT-WG](https://html.spec.whatwg.org/multipage/).  HTML defines the content and structure of a web page.  Other specifications define other aspects of a web page, such as CSS for presentation, and Javascript for interactive behaviour and functionality.

## Basic HTML document structure

All HTML documents have the following structure:

```{code-block} HTML
<!DOCTYPE html>
<html>
   <head>
      <!-- Document metadata goes here -->
   </head>
   <body>
      <!-- Document content goes here -->
   </body>
</html>
```

 * The DOCTYPE directive is a historical vestige of HTML's origin.  For HTML5, this must be present exactly as it appears above to identify to the browser that it is a HTML5-compatible document.

 * The ``<html>`` element is the root element of the entire document.

 * The ``<head>`` element contains the document's metadata.  This is information *about* the document.

 * The ``<body>`` element contains all of the content of the document that will be displayed within the content area of the browser window.

 * HTML comments are contained within the ``<!--`` and ``-->`` delimiters.  These are ignored by the HTML parser.

 ## Elements

 There are two main types of HTML elements - normal elements and void elements.  Normal elements have a start and end tag, between which may go content.  An example is the paragraph element:

 ```{code-block} HTML
<p>Here is a paragraph element</p>
```

Void elements have no content and no end tag.  For example, the line break and image elements.

 ```{code-block} HTML
<p>Here is a paragraph<br>broken over two lines</p>
<img src="foobar.jpg">
```

````{note}
In the past, when HTML was defined as an XML application, void elements required a / character before the terminating bracket of the start tag, to indicate that the element has no content and therefore no end tag.  That is, it's *self-closing*.  For example:

```{code-block} html
<img src="foobar.jpg"/>
```

This is no longer necessary, but is necessary for *foreign elements* that are self-closing, such as embedded MathML or SVG content within a HTML document.
````

## Attributes

Attributes are key/value pairs formatted as ``<key>=<value>`` The value may be surrounded by double or single quotes.  This is optional except when whitespace occurs within the value.  Values may contain normal text as well as character references (therefore be careful of ambiguous ampersands).  Double and single quotes may be part of an attribute's value by inserting the appropriate character reference.

Boolean attributes are an exception to the ``<key>=<value>`` syntax.  They may be presented as just a key with no value.  Just the presence of the key makes the attribute defined and therefore 'true'.  Only the absence of the attribute within the element makes the attribute 'false'.  

If a value is present for a Boolean attribute, it must be either the empty string, or the key itself.  
```{code-block} html
<input type=checkbox disabled>           <!-- Correct -->
<input type=checkbox disabled="">        <!-- Correct -->
<input type=checkbox disabled=disabled>  <!-- Correct -->
<input type=checkbox disabled=foobar>    <!-- Non-conforming -->
<input type=checkbox disabled=true>      <!-- Non-conforming -->
<input type=checkbox disabled=false>     <!-- Non-conforming -->
```

Some attributes have default values which are defined for when an attribute is missing, or when an attribute is invalid.  These values are known as the *missing value default* and the *invalid value default*

## Character references

Character references provide a mechanism for inserting special characters into normal text, such as characters that cannot be written directly (for example, Greek letters when using an ASCII editor) or for escaping special characters (such as \<, \>, and &).

There are three forms of characters references:

 * Named character references, which have the form ``&<name>;``, where ``<name>`` must be a valid named character reference from [this table](https://html.spec.whatwg.org/multipage/named-characters.html#named-character-references).
 * Decimal numeric character references, which have the form ``&#<ddigits>;``, where ``<ddigits>`` is one or more decimal digits forming a valid Unicode code point.
 * Hexadecimal numeric character references, which have the form ``&#[x|X]<hdigits>;`` where ``<hdigits>`` is one or more hexdecimal digits forming a valid Unicode code point.

A 'valid' Unicode code point in this context is any Unicode code point that is not one of the following control characters (0x0000-0x0008, 0x000B and 0x000D) or a [non-character](https://infra.spec.whatwg.org/#noncharacter).