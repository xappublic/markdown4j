

# Getting notified of markdown4j releases #

You can subscribe to markdown4j releases via this [RSS feed](http://code.google.com/feeds/p/markdown4j/downloads/basic).

# Reporting defects or Submiting enhancement requests #

Just send me a message [styrand@gmail.com](mailto:styrand@gmail.com)

# Overview #

markdown4j is an open-source java extensible markdown processor.

It is a fork of the famous https://github.com/rjeschke/txtmark project created by René Jeschke.

It is inspired from the great [John Mac Farlane's Pandoc](http://johnmacfarlane.net/pandoc/) utility which contains a lot of interesting extensions.

It adds somme features, particularly the ability to extend and to modify the rendering of the processor.

List of features :
  * Cross-platform program (100% Java based)
  * Lightweight : no library dependencies, easy to understand and to use
  * Implements the great [John Gruber's incredible Markdown](http://daringfireball.net/projects/markdown/) text-to-html conversion utility.
  * Implements some useful extensions like :
    * strikeout
    * delimited code block
    * newlines conversion
    * address link (to google map)
    * UML diagrams support with two provided plugins : YumlPlugin for class diagrams and WebSequencePlugin for sequence diagrams
    * Ability to customize html rendering (for example add custom attributes like class, style, ...)
    * Ability to extend Makdown4j with plugins
  * Other useful features are planned for the next releases like :
    * toc (table of contents)
    * table
    * numbered headers
    * include

# News #

  * 11/01/2013 : **Markdown4j 2.2 released** :
    * api is made fluent

  * 10/01/2013 : **Markdown4j 2.1 released** :
    * some corrections
    * facilities to customize html rendering

  * 09/01/2013 : **Markdown4j 2.0 released** :
    * some bugs fixes
    * based now on txtmark

  * 07/12/2012 : **Markdown4j 1.1 released** :
    * some bugs fixes

  * 25/10/2012 : **Markdown4j 1.0 released**

# Installing Markdown4j #
  * For the current version of Markdown4j, you will need a [JDK](http://www.oracle.com/technetwork/java/javase/downloads/index.html) version 6 or higher.
  * Download the latest jar distribution of Markdown4j [here](http://code.google.com/p/markdown4j/downloads/list)
  * Add the jar in your classpath


# Using Markdown4j #

You can easily use markdown4j in your program. Just create a Processor then call the markdown method. The processor will parse your markdown text and generate the html block corresponding :

```
import org.markdown4j.Markdown4jProcessor;

...
...

String html = new Markdown4jProcessor().process("This is a **bold** text");
```

# Learning Markdown syntax #

If you want to learn the markdown syntax, just read the [John Gruber's page](http://daringfireball.net/projects/markdown/syntax).

# Markdown extensions #
Markdown4j understands an extended version of [John Gruber’s markdown syntax](http://daringfireball.net/projects/markdown/syntax). This paragraph explains the extensions implemented in markdown4j.

## Strikeout ##

Strikeout is an extension originally created by [John Mac Farlane's Pandoc](http://johnmacfarlane.net/pandoc/).

To strikeout a section of text with a horizontal line, begin and end it with ~~. For example,~~

```
This is ~~deleted~~ text
```

will turn into

```
This is <s>deleted</s> text
```

## Delimited code blocks ##

A delimited code blocks is an extension originally created by [John Mac Farlane's Pandoc](http://johnmacfarlane.net/pandoc/).

These begin with a row of three or more tildes (~) or backticks (`) and end with a row of tildes or backticks that must be at least as long as the starting row. Everything between these lines is treated as code. No indentation is necessary :

```
~~~~~~~
if (a > 3) {
  moveShip(5 * gravity, DOWN);
}
~~~~~~~
```

You can specify the language of the code block:

```
``` haskell
if (a > 3) {
  moveShip(5 * gravity, DOWN);
}
```
```


will turn into

```
<pre><code class="haskell">
if (a > 3) {
  moveShip(5 * gravity, DOWN);
}
</pre></code>
```

## Newlines conversion in paragraph ##

This extension was originally created by [GitHub](http://github.github.com/github-flavored-markdown/).

Markdown4j treats newlines in a paragraph content as real line breaks, which is often what you intended.

```
first line
second line
```

will turn into :

```
<p>first line
<br />second line</p>
```

## Google map address link ##

You can link a section of text containing an address with google map. Just begin it with _<@_ and end it with _>_. For example,

```
<@15 rue de la paix Paris>
```

will turn into

```
<a href="https://maps.google.com/maps?q=15+rue+de+la+paix+Paris" target="_blank">15 rue de la paix Paris</a>
```

## YUML support ##

Markdown supports the creation of UML diagram (class, activity or use case) in your document. This extension uses the famous [yuml](http://www.yuml.me) web service

### Usage ###

```

%%% yuml type=class|activity|usecase scale=numeric style=scruffy|plain|nofunky dir=LR|RL|TD format=png|jpg|svg|json
content here...
%%%

```

For more detail see the [yUML web site](http://www.yuml.me).

### Parameters definition ###

| name | mandatory | type | default value | description |
|:-----|:----------|:-----|:--------------|:------------|
| style| no | string | scruffy | style of the diagram : 'scruffy', 'plain' or 'nofunky'|
| type | no | string | class | type of dthe iagram : 'class', 'usecase' or activity' |
| dir | no | string | LR | direction of the diagram : 'LR', 'RL' or 'TD' |
| format | no | string | png | format of the generated image : 'png', 'jpg' or 'svg' |
| scale | no | int |  | size of the generated image |

### Example ###

```
%%% yuml style=nofunky scale=120 format=svg
[Customer]<>-orders*>[Order] 
[Order]++-0..*>[LineItem]
[Order]-[note:Aggregate root.]
%%%
```


## Websequence support ##

Markdown supports the creation of UML sequence diagram in your document. This extension uses the famous [websequencediagrams](http://www.websequencediagrams.com/) web service

### Usage ###

```

%%% sequence style=default|earth|modern-blue|mscgen|omegapple|qsd|rose|roundgreen|napkin
content here...
%%%

```

For more detail see the [websequencediagrams web site](http://www.websequencediagrams.com/).

### Parameters definition ###

| name | mandatory | type | default value | description |
|:-----|:----------|:-----|:--------------|:------------|
| style| no | string | default | style of the diagram : 'default','earth','modern-blue','mscgen','omegapple','qsd','rose','roundgreen' or 'napkin' |

### Example ###

```
%%% sequence style=modern-blue
title Authentication Sequence

Alice->Bob: Authentication Request
note right of Bob: Bob thinks about it
Bob->Alice: Authentication Response
%%%
```


# Custom HTML rendering #

You can easily customize the html rendering of an HTML element, for example to modify the style of an element.

If you want to display the blockquote in red (set an attribute style to color:red), just add a configuration like this :

```
String html = new Markdown4jProcessor().addHtmlAttribute("style", "color:red", "blockquote").process("...");
```

Just add another parameter if you want to apply this style to another element :

```
String html = new Markdown4jProcessor().addHtmlAttribute("style", "color:red", "blockquote", "h1").process("...");
```

If you want to modify the css class of a and p elements (set an attribute class), just add a configuration like this :

```
String html = new Markdown4jProcessor().addStyleClass("myclass", "a", "p").process("...");
```

If you want to display the blockquote in red (set an attribute target to blank), just add a configuration like this :

```
String html = new Markdown4jProcessor().addHtmlAttribute("target", "_blank", "a").process("...");
```


# Creating your own markdown4j plugin #

Markdown4j allows you to create your own plugin.

A plugin is a block of lines delimited between '%%% ' followed by the name of the plugin and '%%%'. Everything between these lines is treated as plugin.

## Usage ##

```
%%% PluginId param1=value1 param2=value2 ...
Content here ...
%%%
```

## Example ##

```
%%% mypluginid class=classValue type=typeValue
MyPlugInIdContent
...
...
%%%
```

## Instructions ##

To treat theses lines create your own plugin class extending _Plugin_ :

```
public class MyPlugin extends Plugin {
  public MyPlugin() {
    //bind your plugin with id
    super("mypluginid");
  }
  @Override
  public void emit(StringBuilder out, List<String> lines, Map<String, String> params) {
    //read params and manage default value
    String type = params.get("type");
    if(type == null) {
      type = "defaultType";			
    }
    String clazz = params.get("class");
    if(clazz == null) {
      clazz = "defaultClass";			
    }

    //process your plugin and return your text
    out.append("...");
  }
}
```

Then call the _register_ method of the emitter **before** _process_ (the api is fluent) :

```
//Generate html with the custom plugin
String html = new Markdown4jProcessor().register(new MyPlugin()).process("...");
```

# Roadmap #

## Implementation of tables ##

Tables is an extension originally created by [John Mac Farlane's Pandoc](http://johnmacfarlane.net/pandoc/).

It presupposes the use of a fixed-width font, such as Courier.

The table is a block element. It must begin with a line of dashes and must end with a blank line.

Simple tables look like this:
```
--------------  --------- 
         Right  Left
   12                  12
123                 555
```

will turn into

```
<table>
  <tbody>
    <tr class="odd"><td align="right" width="60%">Right</td><td align="left" width="40%">Left</td></tr>
    <tr class="even"><td align="center">12</td><td align="right">12</td></tr>
    <tr class="odd"><td align="left">123</td><td align="center">555</td></tr>
  </tbody>
</table>
```

The headers and table rows must each fit on one line. Column alignments are determined by the position of the text relative to the dashed line below it:
  * If the dashed line is flush with the header text on the right side but extends beyond it on the left, the text is right-aligned.
  * If the dashed line is flush with the header text on the left side but extends beyond it on the right, the text is left-aligned.
  * If the dashed line extends beyond the header text on both sides, the text is centered.
  * If the dashed line is flush with the header text on both sides, the default alignment is used (in most cases, this will be left).

The alignments is calculated for each cell.
The column width is calculated in percent from the number of dashes of each column.


You can add a footer by adding a dashed separator line like this :
```
--------------  --------- 
         Right  Left
   12                  12
123                555
--------------  --------- 
Sum                567
```

will turn into

```
<table>
  <tbody>
    <tr class="odd"><td align="right" width="60%">Right</td><td align="left" width="40%">Left</td></tr>
    <tr class="even"><td align="center">12</td><td align="right">12</td></tr>
    <tr class="odd"><td align="left">123</td><td align="center">555</td></tr>
  </tbody>
  <tfoot>
    <tr class="footer"><td align="left">Sum</td><td align="center">567</td></tr>
  </tfoot>
</table>
```



## TOC (table of content) ##

An inline table of contents can be generated in your page.

### Example ###

```
{{ toc max-depth="2" }}
```

### Parameters definition ###

| name | mandatory | type | description |
|:-----|:----------|:-----|:------------|
| max-depth | no | int | the maximum header depth to display in the table of contents (default : 6) |


## Header identifiers ##

Header identifiers is an extension originally created by [John Mac Farlane's Pandoc](http://johnmacfarlane.net/pandoc/).

Each header element in markdown4j output is given a unique identifier. This identifier is based on the text of the header. To derive the identifier from the header text,
  * Remove all formatting, links, etc.
  * Remove all punctuation, except underscores, hyphens, and periods.
  * Replace all spaces and newlines with hyphens.
  * Convert all alphabetic characters to lowercase.
  * Remove everything up to the first letter (identifiers may not begin with a number or punctuation mark).
  * If nothing is left after this, use the identifier section.

These identifiers are used to provide links from one section of a document to another. A link to this section, for example, might look like this :

```
This is h1 section
=============

My h1 content.

This is h2 section
-------------

My h2 content.

######## This is h3 section ########

My h3 content [See h2 section](#this-is-h2-section)

```

## Numbered Headers ##

Numbered headers is a useful rendering extension to add a number before your header title.

Just call the _numberHeaders_ method of the processor **before** _markdown_ (the api is fluent).

```
MarkdownProcessor processor = new MarkdownProcessor();
//Generate html with numbered headers
String html = processor.numberHeaders().markdown(...);
```

## Ignore first header ##

Sometimes the first header is the title of your document : you want to ignore it in the toc and in the numbering of the headers.

Just call the _ignoreFirstHeader_ method of the processor **before** _markdown_ (the api is fluent).

```
MarkdownProcessor processor = new MarkdownProcessor();
//Generate html with numbered headers and ignore first header
String html = processor.numberHeaders().ignoreFirstHeader().markdown(...);
```

## Include extension ##

Include another markdown document into the current document.

### Example ###

```
...
{{include src="https://raw.github.com/vmg/redcarpet/4c14d0875163890e553897efcceb7480aa34f8e9/README.markdown"}}
...
```

### Parameters definition ###

| name | mandatory | type | description |
|:-----|:----------|:-----|:------------|
| src| yes | string | path of the document to include (can be an url or a relative path) |

