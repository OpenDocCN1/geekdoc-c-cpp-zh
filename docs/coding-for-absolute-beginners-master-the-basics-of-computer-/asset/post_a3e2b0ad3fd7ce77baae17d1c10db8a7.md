
```html
<frameset rows = "10%,80%,10%">
    <frame name = "top" src = "/html/top_frame.htm" />
    <frame name = "main" src = "/html/main_frame.htm" />
    <frame name = "bottom" src = "/html/bottom_frame.htm" />

    <noframes>
    <body>Your browser does not support frames.</body>
    </noframes>

</frameset>
</html>
```

### iFrame

To create a nested browsing context, iFrame tag can be used to add a new HTML document into an existing one. To create an iFrame, the following syntax can be implemented along with the `<iframe>` tag:

```html
<iframe src="https://www.samplewebsite.com"></iframe>
```

Complete table of basic HTML tags:

|  |  |  |  |  |
|---|---|---|---|---|
| `<a>` | `<abbr>` | `<acronym>` | `<address>` | `<applet>` |
| `<area>` | `<article>` | `<aside>` | `<audio>` | `<b>` |
| `<base>` | `<basefont>` | `<bdi>` | `<bdo>` | `<big>` |
| `<blockquote>` | `<body>` | `<br>` | `<button>` | `<canvas>` |
| `<caption>` | `<center>` | `<cite>` | `<code>` | `<col>` |
| `<colgroup>` | `<data>` | `<datalist>` | `<dd>` | `<del>` |
| `<details>` | `<dfn>` | `<dialog>` | `<dir>` | `<div>` |
| `<dl>` | `<dt>` | `<em>` | `<embed>` | `<fieldset>` |
| `<figcaption>` | `<figure>` | `<font>` | `<footer>` | `<form>` |
| `<frame>` | `<frameset>` | `<h1> - <h6>` | `<head>` | `<header>` |
| `<hr>` | `<html>` | `<i>` | `<iframe>` | `<img>` |
| `<input>` | `<ins>` | `<kbd>` | `<label>` | `<legend>` |
| `<li>` | `<link>` | `<main>` | `<map>` | `<mark>` |
| `<meta>` | `<meter>` | `<nav>` | `<noframes>` | `<noscript>` |
| `<object>` | `<ol>` | `<optgroup>` | `<option>` | `<output>` |
| `<p>` | `<param>` | `<picture>` | `<pre>` | `<progress>` |
| `<q>` | `<rp>` | `<rt>` | `<ruby>` | `<s>` |
| `<samp>` | `<script>` | `<section>` | `<select>` | `<small>` |
| `<source>` | `<span>` |  | `<strong>` | `<style>` |
| `<sub>` | `<summary>` | `<sup>` | `<svg>` | `<table>` |
| `<tbody>` | `<td>` | `<template>` | `<textarea>` | `<tfoot>` |
| `<th>` | `<thead>` | `<time>` | `<title>` | `<tr>` |
| `<track>` | `<tt>` | `<u>` | `<ul>` | `<var>` |
| `<video>` | `<wbr>` |  |  |  |

## Forms

HTML forms are one of the key aspects of interaction between a website and a user. A form is created by using widgets such as text fields, buttons, select boxes, radio buttons, file select boxes, hidden controls, and clickable controls. Data collected through forms is sent to the web server and the web page can also intercept the data on its own. Most of the times, widgets are linked with a label in order to describe their purpose.

Syntax for creating a form in HTML:

```html
<form action = "Script URL" method = "GET|POST">
    form elements like input, buttons etc.
</form>
```

Input form to take Name and Age from user:

```html
<html>

    <head>
        <title>My first HTML form</title>
    </head>

    <body>
        <form>
            Name: <input type = "text" name = "Name" />
            <br>
            Age: <input type = "text" name = "last name" />
        </form>
    </body>
</html>
```

Output:

![](img/9d932bec53e523b8d8b7b8134cf77ca7_114_0.png)

### Text Fields

Text fields in HTML allow users to input text into the form. The general syntax for creating text fields is defined as follows:

```html
<input type = "text" value = "text">
```

### Button controls

There are different ways to submit data into forms. We can add clickable buttons by using the following HTML tags:

```html
<input type = "submit" name = "submit" value = "Submit" />
<input type = "reset" name = "reset" value = "Reset" />
<input type = "button" name = "button" value = "button" />
```

Output:

![](img/9d932bec53e523b8d8b7b8134cf77ca7_114_1.png)

### Select box

To create a dropdown list in HTML forms, we can use the `<select>` and `<option>` element.

For example:

```html
<html>
    <head>
        <title>File Upload Box</title>
    </head>
    <body>
        <form>
            <label for="Course">Course:</label>
            <select name="Course" id="course">
                <option value="Web Engineering">Web Engineering</option>
                <option value="Calculus">Calculus</option>
                <option value="Data Science">Data Science</option>
            </select>
        </form>
    </body>
</html>
```

Output:

![](img/9d932bec53e523b8d8b7b8134cf77ca7_115_0.png)

### Select Box

The Select Box element gives an option to list down multiple options in HTML form.

For example:

```html
<html>
    <head>
        <title>Select your course</title>
    </head>

    <body>
        <form>
            <select name = "dropdown">
                <option value = "Math" selected>Math</option>
                <option value = "Physics">Physics</option>
            </select>
        </form>
    </body>
</html>
```

Output:

![](img/9d932bec53e523b8d8b7b8134cf77ca7_116_0.png)

### Form Element

Once the HTML form has been completed, the two attributes Action and Method are required to store and send form data. Action contains the address which defines where the form data will be sent whereas Method can either be GET or POST as it defines how to handle form information. The syntax for creating Form element is defined as follows:

```html
<form action = "/login" method = "POST">
```

## Designing

In HTML, the default background color for any webpage is white. To change the background color, the following tags and attributes can be used:

```html
<tagname bgcolor = "color value/color name">
```

For example:

```html
<table bgcolor = "green">
<table bgcolor = "#f1f1f1">
```

### Fonts

Fonts are an essential part of any website and enhance the readability of your content. The `<font>` tag can be used to give a specific style, size, and color to the text and its attributes include size, color, and face.

To set the font size, the tags and attributes are:

```html
<font size = "14"> Text </font>
```

Font face tags and attributes:

```html
<font face = "Times New Roman" size = "14"> Text </font>
```

### Font color

To change the font color, the following HTML tags and attributes can be used:

```html
<html>
    <head>
        <title>Setting Font Color</title>
    </head>

    <body>
        <font color = "Blue">This text is blue</font>
    </body>
</html>
```

Output: **This text is blue**

### Marked text

The text written between `<mark>` and `</mark>` elements is displayed as marked with yellow.

For example:

```html
<p> This text is marked as <mark> Yellow </mark> </p>
```

Output: This text is marked as **Yellow**.

### Meta Tags

In HTML, meta tags can be used to add metadata into your web pages. The attributes of meta tags include Name, Content, Scheme, and http-equiv. We can use `<meta>` tag to give a short description about the document which can also improve search engine indexing for your web page.

For example:

```html
<html>

    <head>
        <title>Meta Tags Example</title>
        <meta name = "keywords" content = "HTML, Meta Tags, Metadata" />

        <meta name = "description" content = "Meta Tags." />
        <meta name = "revised" content = "3/7/2019" />
        <meta http-equiv = "cookie" content = "userid = abc; expires = Monday, 08-Sep-19 23:59:59 GMT;" />

    </head>
    <body>
        <p>Welcome to HTML</p>
    </body>

</html>
```

### Comments

To place comments in HTML code, the following syntax can be followed:

```html
<html>
    <head> <!-- Document Header Starts -->
        <title>Document title</title>
    </head> <!-- Document Header Ends -->
    <body>
        <p>Document content goes here.....</p>
    </body>
</html>
```

### HTML Style Sheets

For further design of HTML documents, Cascading Style Sheets (CSS) are implemented over the website. They provide easy, effective, and manageable alternatives to specify certain attributes for a website. We will be discussing CSS in full detail in the next chapter.

### Layout and Responsiveness

HTML includes various types of semantic elements that are used to define different parts of a web page. These elements include Header, Container, Section, Article, Aside, Details, and Footer. Although CSS is the best approach to design layout of a web page, we can also complete the procedure through these HTML elements.

A responsive web design is created by using HTML and CSS. This procedure automatically resizes and adjusts a website to make it look suitable on all devices such as desktop, smartphone, and tablet. For more details regarding responsiveness, learning about CSS and Bootstrap language will prove to be of great advantage.
