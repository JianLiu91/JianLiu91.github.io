title: Hello World
layout: post
date: 2015-07-31 19:07:43
comments: true
categories: Blog
tags: [Markdown]
keywords: Markdown, Blog
description: Markdown syntax, just for test.
---
# Mou

![Mou icon](http://mouapp.com/Mou_128.png)

<!-- more -->

## Overview

**Mou**, the missing Markdown editor for *web developers*.

### Syntax

#### Strong and Emphasize 

**strong** or __strong__ ( Cmd + B )

*emphasize* or _emphasize_ ( Cmd + I )

**Sometimes I want a lot of text to be bold.
Like, seriously, a _LOT_ of text**

#### Blockquotes

> Right angle brackets &gt; are used for block quotes.

#### Links and Email

An email <example@example.com> link.

Simple inline link <http://chenluois.com>, another inline link [Smaller](http://smallerapp.com), one more inline link with title [Resize](http://resizesafari.com "a Safari extension").

A [reference style][id] link. Input id, then anywhere in the doc, define the link with corresponding id:

[id]: http://mouapp.com "Markdown editor on Mac OS X"

Titles ( or called tool tips ) in the links are optional.

#### Images

An inline image ![Smaller icon](http://smallerapp.com/favicon.ico "Title here"), title is optional.

A ![Resize icon][2] reference style image.

[2]: http://resizesafari.com/favicon.ico "Title"

#### Inline code and Block code

Inline code are surround by `backtick` key. To create a block code:

  Indent each line by at least 1 tab, or 4 spaces.
    var Mou = exactlyTheAppIwant; 

####  Ordered Lists

Ordered lists are created using "1." + Space:

1. Ordered list item
2. Ordered list item
3. Ordered list item

#### Unordered Lists

Unordered list are created using "*" + Space:

* Unordered list item
* Unordered list item
* Unordered list item 

Or using "-" + Space:

- Unordered list item
- Unordered list item
- Unordered list item

#### Hard Linebreak

End a line with two or more spaces will create a hard linebreak, called `<br />` in HTML. ( Control + Return )  
Above line ended with 2 spaces.

#### Horizontal Rules

Three or more asterisks or dashes:

***

---

- - - -

#### Headers

Setext-style:

This is H1
==========

This is H2
----------

atx-style:

# This is H1
## This is H2
### This is H3
#### This is H4
##### This is H5
###### This is H6


### Extra Syntax

#### Footnotes

Footnotes work mostly like reference-style links. A footnote is made of two things: a marker in the text that will become a superscript number; a footnote definition that will be placed in a list of footnotes at the end of the document. A footnote looks like this:

That's some text with a footnote.[^1]

[^1]: And that's the footnote.


#### Strikethrough

Wrap with 2 tilde characters:

~~Strikethrough~~


#### Fenced Code Blocks

Start with a line containing 3 or more backticks, and ends with the first line with the same number of backticks:

```
Fenced code blocks are like Stardard Markdown’s regular code
blocks, except that they’re not indented and instead rely on
a start and end fence lines to delimit the code block.
```

#### Tables

A simple table looks like this:

First Header | Second Header | Third Header
------------ | ------------- | ------------
Content Cell | Content Cell  | Content Cell
Content Cell | Content Cell  | Content Cell

If you wish, you can add a leading and tailing pipe to each line of the table:

| First Header | Second Header | Third Header |
| ------------ | ------------- | ------------ |
| Content Cell | Content Cell  | Content Cell |
| Content Cell | Content Cell  | Content Cell |

Specify alignement for each column by adding colons to separator lines:

First Header | Second Header | Third Header
:----------- | :-----------: | -----------:
Left         | Center        | Right
Left         | Center        | Right


### Shortcuts

#### View

* Toggle live preview: Shift + Cmd + I
* Toggle Words Counter: Shift + Cmd + W
* Toggle Transparent: Shift + Cmd + T
* Toggle Floating: Shift + Cmd + F
* Left/Right = 1/1: Cmd + 0
* Left/Right = 3/1: Cmd + +
* Left/Right = 1/3: Cmd + -
* Toggle Writing orientation: Cmd + L
* Toggle fullscreen: Control + Cmd + F

#### Actions

* Copy HTML: Option + Cmd + C
* Strong: Select text, Cmd + B
* Emphasize: Select text, Cmd + I
* Inline Code: Select text, Cmd + K
* Strikethrough: Select text, Cmd + U
* Link: Select text, Control + Shift + L
* Image: Select text, Control + Shift + I
* Select Word: Control + Option + W
* Select Line: Shift + Cmd + L
* Select All: Cmd + A
* Deselect All: Cmd + D
* Convert to Uppercase: Select text, Control + U
* Convert to Lowercase: Select text, Control + Shift + U
* Convert to Titlecase: Select text, Control + Option + U
* Convert to List: Select lines, Control + L
* Convert to Blockquote: Select lines, Control + Q
* Convert to H1: Cmd + 1
* Convert to H2: Cmd + 2
* Convert to H3: Cmd + 3
* Convert to H4: Cmd + 4
* Convert to H5: Cmd + 5
* Convert to H6: Cmd + 6
* Convert Spaces to Tabs: Control + [
* Convert Tabs to Spaces: Control + ]
* Insert Current Date: Control + Shift + 1
* Insert Current Time: Control + Shift + 2
* Insert entity <: Control + Shift + ,
* Insert entity >: Control + Shift + .
* Insert entity &: Control + Shift + 7
* Insert entity Space: Control + Shift + Space
* Insert Scriptogr.am Header: Control + Shift + G
* Shift Line Left: Select lines, Cmd + [
* Shift Line Right: Select lines, Cmd + ]
* New Line: Cmd + Return
* Comment: Cmd + /
* Hard Linebreak: Control + Return

#### Edit

* Auto complete current word: Esc
* Find: Cmd + F
* Close find bar: Esc

#### Post

* Post on Scriptogr.am: Control + Shift + S
* Post on Tumblr: Control + Shift + T

#### Export

* Export HTML: Option + Cmd + E
* Export PDF:  Option + Cmd + P


### And more?

Don't forget to check Preferences, lots of useful options are there.

Follow [@chenluois](http://twitter.com/chenluois) on Twitter for the latest news.

For feedback, use the menu `Help` - `Send Feedback`

-------

The freemind theme offers several new tag plugins, so as to fully take advantages of Bootstrap.

To use these tag plugins, you need to install [hexo-tag-bootstrap](https://github.com/wzpan/hexo-tag-bootstrap) first. In your blog root folder, execute the following command:

```
$ npm install hexo-tag-bootstrap --save
```

Then you can use these tag plugins in your blog, as easily as you normally do using hexo tag plugins. 

<!-- more -->

## Text Color ##

Convey meaning through color with a handful of emphasis utility classes. These may also be applied to links and will darken on hover just like our default link styles.

### Syntax ###

```
{% textcolor [style] %}
  text string
{% endtextcolor %}
```

### Examples ###

```
{% textcolor muted %}Fusce dapibus, tellus ac cursus commodo, tortor mauris nibh.{% endtextcolor %}

{% textcolor primary %}Nullam id dolor id nibh ultricies vehicula ut id elit.{% endtextcolor %}

{% textcolor success %}Duis mollis, est non commodo luctus, nisi erat porttitor ligula.{% endtextcolor %}

{% textcolor info %}Maecenas sed diam eget risus varius blandit sit amet non magna.{% endtextcolor %}

{% textcolor warning %}Etiam porta sem malesuada magna mollis euismod.{% endtextcolor %}

{% textcolor danger %}Donec ullamcorper nulla non metus auctor fringilla.{% endtextcolor %}
```

### Results ###

{% textcolor muted %}Fusce dapibus, tellus ac cursus commodo, tortor mauris nibh.{% endtextcolor %}

{% textcolor primary %}Nullam id dolor id nibh ultricies vehicula ut id elit.{% endtextcolor %}

{% textcolor success %}Duis mollis, est non commodo luctus, nisi erat porttitor ligula.{% endtextcolor %}

{% textcolor info %}Maecenas sed diam eget risus varius blandit sit amet non magna.{% endtextcolor %}

{% textcolor warning %}Etiam porta sem malesuada magna mollis euismod.{% endtextcolor %}

{% textcolor danger %}Donec ullamcorper nulla non metus auctor fringilla.{% endtextcolor %}

## Buttons ##

Inserts a button with target links, text and specified color.

### Syntax ###

```
{% btn url text [style] %}
```

### Examples ###

```
{% btn http://hahack.com hahack %}

{% btn http://hahack.com hahack primary %}

{% btn http://hahack.com hahack success %}

{% btn http://hahack.com hahack warning %}

{% btn http://hahack.com hahack danger %}

{% btn http://hahack.com hahack info %}
```

### Results ###

{% btn http://hahack.com hahack %}

{% btn http://hahack.com hahack primary %}

{% btn http://hahack.com hahack success %}

{% btn http://hahack.com hahack warning %}

{% btn http://hahack.com hahack danger %}

{% btn http://hahack.com hahack info %}

## Labels ##

Inserts a label with text and specified color.

### Syntax ###

```
{% label text [style] %}
```

### Examples ###

```
{% label default %}

{% label warinng warning %}

{% label success success %}

{% label danger danger %}

{% label primary primary %}

{% label info info %}
```

### Results ###

{% label default %}

{% label warinng warning %}

{% label success success %}

{% label danger danger %}

{% label primary primary %}

{% label info info %}

## Badges ##

Inserts a badge with text.


### Syntax ###

```
{% badge text %}
```

### Examples ###

```
{% badge 42 %}
```

### Results ###

{% badge 42 %}

## Alerts ##

Inserts alert messages with text and specified color.

### Syntax ###

```
{% alert [style] %}
   Alert string
{% endalert %}
```

### Examples ###

```
{% alert warning %}Best check yo self, you're not looking too good.{% endalert %}

{% alert danger %}Change a few things up and try submitting again.{% endalert %}

{% alert success %}You successfully read this important alert message.{% endalert %}

{% alert info %}This alert needs your attention, but it's not super important.{% endalert %}
```

### Results ###

{% alert warning %}Best check yo self, you're not looking too good.{% endalert %}

{% alert danger %}Change a few things up and try submitting again.{% endalert %}

{% alert success %}You successfully read this important alert message.{% endalert %}

{% alert info %}This alert needs your attention, but it's not super important.{% endalert %}

------

{% label Q danger %} What does `Freemind` stands for?

{% label A success %} `Freemind` is named after [Pluskid's blog](http://freemind.pluskid.org/). This theme is greatly inspired by his blog layouts and stylesheets.

{% label Q danger %} There're already so many themes for Hexo. Why create this one?

{% label A success %} In fact I created this theme before I turned to use Hexo. I switched to Hexo about half an year ago, including my theme, since I have already got used to it and don't wanna change it for now.

{% label Q danger %} Why use raw CSS stylesheets instead of more fashionable stylus?

{% label A success %} Yes, stylus is cool. But I don't want to wrote my stylesheets again in stylus. So let's just keep them.

{% label Q danger %} I love your theme. How to contribute?

{% label A success %} Great that you love it. To devote your contribution, you can:

* Star its [Github project](https://github.com/wzpan/hexo-theme-freemind);
* Fork this project, make your change, and then send me your pull request;
* Since it is public under MIT license, you can make your own theme based on mine. But it will be nicer if you claimed that your work is based on mine in your theme project page.

{% label Q danger %} [Your blog](http://hahack.com) looks a little different to this theme. Why such difference?

{% label A success %} Yes. I modified the theme a little bit as I open sourced this theme. I actually did some simplification *e.g.* I removed the whole [Wiki](http://hahack.com/wiki) page because I don't think that everybody need this.

{% label Q danger %} How to generate ToC(Table of Contents) in a certain page?

{% label A success %} Add `toc: true` in the [front-matter](https://github.com/wzpan/hexo-theme-freemind#front-matter).

{% label Q danger %} Where can I find your markdown source files of these docs?

{% label A success %} In the [source](https://github.com/wzpan/hexo-theme-freemind/tree/source) branch.

{% label Q danger %} Why my boostrap tags always break lines? How to avoid that?

{% label A success %} The problem is due to the markdown settings. Try to disable the `breaks` config in your root _config.yml. *e.g.*

-----


大家都喜欢用 $E=mc^2$ 举例子，但是我不是很理解。  

这个公式 $\cos 2\theta = \cos^2 \theta - \sin^2 \theta =  2 \cos^2 \theta - 1$ 少年可还记得？

插入方程组（注意多行公式结尾\\\需要打成\\\，可能是因为markdown会自动转义第一个\\）：

\begin{aligned}
\dot{x} & = \sigma(y-x) \\\
\dot{y} & = \rho x - y - xz \\\
\dot{z} & = -\beta z + xy
\end{aligned}

插入矩阵（同上）：

\begin{bmatrix}
1 & 2\\\
3 & 4
\end{bmatrix}

来个复杂点的（注意有的公式开头不会自动识别，用$$包围）：

$$\frac{\partial u}{\partial t}
= h^2 \left( \frac{\partial^2 u}{\partial x^2} +
 \frac{\partial^2 u}{\partial y^2} + 
 \frac{\partial^2 u}{\partial z^2}\right)$$

最后来个牛逼的吧，薛定谔方程，大学物理就记得这个了：

$$ i\hbar\frac{\partial \psi}{\partial t}
= \frac{-\hbar^2}{2m} \left(
\frac{\partial^2}{\partial x^2} + 
 \frac{\partial^2}{\partial y^2} +
 \frac{\partial^2}{\partial z^2} 
\right) \psi + V \psi.$$