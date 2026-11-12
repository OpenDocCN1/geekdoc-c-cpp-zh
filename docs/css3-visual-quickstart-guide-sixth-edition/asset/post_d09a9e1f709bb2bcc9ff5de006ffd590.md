
## Code 3.9 chapter01.html-- The chaptertitle class is used to style chapter titles where they appear

```html
<!-- HTML5 -->
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<title>Alice&#8217;s Adventures in Wonderland</title>
<link href="global.css" type="text/css" rel="stylesheet" media="all">
<link href="ch01.css" rel="stylesheet" type="text/css" media="all">
<style type="text/css" media="all">
h1 {
    color: orange;
    font-size: 3em;
    font-weight: normal; }
h1 .chaptertitle {
    color: yellow;
    font-size: .5em; }
p {
    color: rgb(153,153,153);
    font-family: perpetua, georgia, serif;
    line-height: 1.5;
    text-indent: 3em; }
.chaptertitle {
    font-family: perpetua, georgia, serif;
    letter-spacing: .1em;
}
a.chaptertitle {
    font-size: 2em;
    font-style: italic;
    letter-spacing: auto;
}
</style>
</head>
<body>
<h1 style="color:red;">Alice&#8217;s Adventures in Wonderland</h1>
<h1 id="ch01">Chapter 1 <span class="chaptertitle">Down the Rabbit-Hole</span></h1>
<p><strong>Alice was beginning to get very tired of sitting by her sister on the bank, and of having nothing to do: once or twice she had peeped into the book her sister was reading, but it had no pictures or conversations in it, "and what is the use of a book," thought Alice, "without pictures or conversations?"</strong></p>
<footer><nav> Next: <a class="chaptertitle" href="AAIWL-ch02.html">The Pool of Tears</a>
</nav></footer>
</body>
</html>
```

- 4. Add the class attribute to the HTML tag to which you want to apply it.

```html
<span class="chaptertitle">Down the Rabbit-Hole</span>
```

```html
<a class="chaptertitle" href="AAIWL-ch02.html">The Pool of Tears</a>
```

You can apply multiple classes to a single HTML tag by adding additional class names in a space separated list: class="name1 name2 names"

Notice that when you defined the class in the CSS, it began with a period (.). However, you do not use the period when referencing the class name in an HTML tag. Using a period here will cause the class to fail.

TIP You can mix a class with ID and/or inline rules within an HTML tag. (See "Inline: Adding Styles to an HTML Tag" and "Defining Unique IDs" in this chapter.)

TIP Because the <div> and <span> tags have no preexisting properties, you can use them to effectively create your own HTML tags by adding classes. However, use these sparingly because once they are associated, you are locked in to using those specific classes with those specific locations.

```css
#ch01 {
 color: red;
 font-size: 3em;
 font-weight: normal;
 }

<h1 id="ch01">...</h1>
```

The general syntax for an ID selector rule.

## Defining Unique IDs

Like the class selector, the ID selector can be used to create unique styles that are independent of any particular HTML tag. Thus, they can be assigned to any HTML tag. IDs are used in HTML to help establish the structure of your page layout, identifying unique elements in the code, singling them out for special treatment, either for positioning with CSS or JavaScript.

### To define an ID selector:

- 1. Add the ID selector to your CSS. ID rules always start with a number sign (#) followed by the name of the ID (Code 3.10).

```css
#ch01 {...}
```

The name can be a word or any set of letters or numbers you choose, with the following caveats:

- Use only letters and numbers. You can use hyphens and underscores, but do so with caution. Some earlier browsers reject them.
- The first character cannot be a number, hyphen, or underscore.
- Don't use spaces.

CSS rules can be defined in the head of your document within the <style> tags or in an external CSS file that is imported or linked to the HTML document.

- 2. Add declarations to your ID. Within the curly brackets, type the style declarations to be assigned to this ID—formatted as property: value—using a semicolon (;) and separating individual declarations in the list. You can also add one or more line breaks, spaces, or tabs after a declaration without interfering with the code to make it more readable.

```css
font-family: perpetua, georgia, serif;
```

```css
text-shadow: 4px 4px 6px rgba(0,0,0,.5);
```

- 3. Add the id attribute to the HTML tag of your choice, with the name of the ID as its value.

```html
<h1 id="ch01">...</h1>
```

Notice that although the number sign (#) is used to define an ID selector, it is not included for referencing the ID in the HTML tag. If you add it, the rule will fail.

![](img/e1ed1e3c1873fa9fc855210fb83699d0_79_0.png)

The results of Code 3.10. The chapter title is using perpetua with a drop shadow.

```html
<!-- HTML5 -->
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<title>Alice's Adventures in Wonderland</title>
<link href="Alice&#8217;s.css" type="text/css" rel="stylesheet" media="all">
<link href="ch01.css" rel="stylesheet" type="text/css" media="all">
<style type="text/css" media="all">
h1 {
color: orange;
font-size: 3em;
font-weight: normal; }
h1 .chaptertitle {
color: yellow;
font-size: .5em; }
p {
color: rgb(153,153,153);
font-family: perpetua, georgia, serif;
line-height: 1.5;
text-indent: 3em; }
.chaptertitle {
font-family: perpetua, georgia, serif;
letter-spacing: .1em; }
a.chaptertitle {
font-size: 2em;
font-style: italic;
letter-spacing: auto; }
#ch01 {
font-family: perpetua, georgia, serif;
text-shadow: 0 4px rgba(0,0,0,.75); }
</style>
</head>
<body>
<h1 style="color:red;">Alice&#8217;s Adventures in Wonderland</h1>
<h1 id="ch01">Chapter 1 <span class="chaptertitle">Down the Rabbit-Hole</span></h1>
<p><strong>Alice was beginning to get very tired of sitting by her sister on the bank, and of having nothing to do: once or twice she had peeped into the book her sister was reading, but it had no pictures or conversations in it, "and what is the use of a book," thought Alice, without pictures or conversations?</strong></p>
<footer><nav> Next: <a class="chaptertitle" href="AAIWL-ch02.html">The Pool of Tears</a>
</nav></footer>
</body>
</html>
```

TIP You can also create dependent IDs, which use the declarations of the ID only when applied to a particular HTML tag. However, I never have a use for these because the point of IDs is that you use them only once per page.

TIP Although you can use the same name for both a class and ID, you should try to avoid this because it will inevitably lead to confusion.

TIP You can mix an ID with a class and/or inline rules within an HTML tag.

TIP IDs can give each screen element a unique name and identity. This is why an ID is used only once, for one element in a document, to make it an object that can be manipulated with JavaScript.

```
HTML selector
ID selector Declaration
h1#ch01 {
color: red;
font-size: 3em;
font-weight: normal; }
<h1 id="ch01">...</h1>
ID attribute
```

The general syntax for the dependent ID selector rule.

```css
* {
  color: red;
  font-size: 3em;
  font-weight: normal; }
```

The general syntax for the universal selector rule.

## Defining Universal Styles

The universal selector is a wildcard character that works as a stand-in to represent any HTML type selector that can appear in that position in a contextual list (A).

Keep in mind, though, that the universal selector can be used in place of any HTML selector in any configuration, not just as a stand alone selector as shown in this section. The usefulness of this will become apparent in the next chapter when you use contextual styles.

### To use the universal selector:

- 1. Add the universal selector. Type an asterisk (*) and then the open curly bracket (Code 3.11). This selector is then a wildcard that can be any HTML tag.

```css
* {...}
```

- 2. Add declarations to your universal selector rule. Within the curly brackets, type the style declarations to be assigned to this ID—formatted as property: value—using a semicolon (;) and separating individual declarations in the list. You can also add one or more line breaks, spaces, or tabs after a declaration without interfering with the code to make it more readable.

```css
margin: 0; padding: 0;
```

In this format, the styles are applied to every element on the page.
