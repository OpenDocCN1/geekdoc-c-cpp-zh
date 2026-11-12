
**TIP** You can also type a space and add another text-decoration value (Table 6.13). As long as the first value is not none, you can use multiple text decorations by adding more values in a list separated by spaces, as follows: overline underline line-through

**TIP** Ding dong, the blink is dead. With CSS3, the blink value has been officially removed as a text decoration option, and the <blink> HTML tag is long gone. Now if you want to annoy your visitors with blinking text, you'll have to use Adobe Flash.

**TIP** Text decorations are applied across an entire text block element rather than on a letter-by-letter basis. This means that a child element cannot override the text decoration set by its parent.

**TIP** Although a child element cannot override its parent's text decoration, child elements can have additional text decoration added to them. In the example, notice that the emphasis tag uses strikethrough, which is added to the underlining already supplied by the paragraph tag.

**TIP** Striking through text is useful for text that you want to show as deleted. For example, I've used strikethrough in online catalogs that include sale prices. I show the original price in strikethrough with the sale price next to it. That said, using the <del> tag is a better option because it communicates deletion.

**TIP** Honestly, the only time I use text decoration is to turn off hypertext link underlining. Underlining is just too indiscriminate, placing a hard line under the text in the same color as the text. Some work is being done to provide more underline control to set the space, color, and style of the underline.

### Underlining Links?

Setting text-decoration: none; in the <a> tag overrides the underline in hypertext links, even if the visitor's browser is set to underline links. In my experience, many visitors look for underlining to identify links. Although I don't like underlining for links—it clutters the page, and CSS offers many superior alternatives—I receive angry emails from visitors when I turn off underlining.

One alternative to the text-decoration property is to use the border-bottom property with the link tag to provide faux underlining. This gives you much better control over the underline appearance, and it even allows you to use different colors.

### Coming Soon!

Several text properties are still under development by the W3C and have yet to be substantially implemented in browsers. You may see them soon, but at the time of this writing I can't give a specific way to implement them across browsers:

**Outlining text**—Adding an outline around the text (also called a *text stroke*) is another way to make text distinctive, most often for titles. Webkit already includes a rudimentary property for this, but the syntax is likely to change in the final W3C version.

**Kerning**—Remember that letter spacing is not kerning. The new *font-kerning* property will provide some rudimentary kerning capabilities.

**Hanging punctuation**—One common problem in typography is what to do when alphanumeric characters are not present at the beginning of a block of text, as with quotation marks. The *hanging-punctuation* property will allow you to define how these characters are treated, either placing them in the edge of the text block or outside.

**Text line decoration**—As mentioned in my explanation of the *text-decoration* property, several new associated properties are being developed to style the text decoration, including *text-line-color*, *text-line-style*, *text-line-skip*, and *text-underline-position*.

To follow the development of these styles, visit the CSS3 Text Module at www.w3.org/TR/css3-text.

### Putting It All Together

Code 6.12 Shows the final results for the file text-properties.css, which we have been building this chapter.

Code 6.12 text-properties.css in its entirety.

```
/*** text-properties.css ***/
body {
    line-height: 1.5; }
h1 {
    letter-spacing: -.05em;
    word-spacing: -1em;
    line-height: .9em;
    text-shadow: 2px 3px 5px rgba(0,0,0,.75); }
h2 {
    letter-spacing: 2px;
    word-spacing: 3px;
    line-height: 1em;
    text-align: center; }
header h2 {
    text-align: right; }
article h2 {
    text-shadow: 0px 1px 1px rgba(255,255,255,.6), 0px -1px 1px rgba(0,0,0,.6); }
h2 .chaptertitle {
    letter-spacing: 0;
    vertical-align: middle; }
p {
    line-height: 2em;
    text-align: justify;
    text-indent: 3em; }
h2 + p {
    text-indent: 0; }
h2 + p:first-letter {
    letter-spacing: -.05em;
    line-height: 24px;
    text-shadow: -3px -3px 3px rgba(153,0,0,.9), 2px 3px 5px rgba(0,0,0,.5); }
address, blockquote {
    text-transform: uppercase;
    white-space: pre; }
a {
    text-decoration: none; }
.delete {
    text-decoration: line-through; }
.pageheader h2 {
    word-spacing: -3em;
    text-align: right; }
.pageheader h2 cite {
    word-spacing: 0;
    text-transform: uppercase;
    vertical-align: -.6em; }
```

## Color and Background Properties

Colors form the cornerstone of all design, even if they're only black and white. They create the first impression of your site. Bright, vibrant, jewel-like colors make a radically different statement than earth tones. Even if you choose to use only black and white, your design will make a statement. Beyond their decorative impact, colors can also guide the viewer's eye around the page, helping to highlight some important areas while downplaying others. In this chapter, you will learn the primary methods used to add and control color with CSS. Keep in mind, however, you can specify color using several CSS properties. (See the sidebar “Other Ways to Add Color.”) But before you learn how to code colors, let's quickly explore how to choose them.

### In This Chapter

- Getting Started 184
- Choosing Color Values 185
- Creating Color Gradients 191
- Choosing Your Color Palette 196
- Setting Text Color 202
- Setting a Background Color 204
- Setting Background Images 205
- Using Background Shorthand to Add Multiple Background Images and Gradients 212
- Putting It All Together 217

### Getting Started

I'll be pulling the sample code for this chapter from Chapter 3 of Alice's Adventures in Wonderland. An expurgated version is shown in Code 71, including a navigational footer at the bottom. It imports the final CSS code from Chapters 5 and 6, and imports a new file called color-background-properties.css, that will contain the CSS code from this chapter.

### Code 71 The HTML5 code used for the examples in this chapter.

```html
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="utf-8">
<title>Alice&amp;#8217;s Adventures In Wonderland | Chapter III</title>
<link href="..."css/font-properties.css" type="text/css" rel="stylesheet" media="all">
<link href="..."css/text-properties.css" type="text/css" rel="stylesheet" media="all">
<link href="..."css/color-background-properties.css" type="text/css" rel="stylesheet" media="all">
<link href="..."css/color-background-properties.css" type="text/css" rel="stylesheet" media="all">
</head>
<body id="chapter3" class="book aaw chapter">
<header class="page">
<hgroup>
<h1>Alice&amp;#8217;s Adventures in Wonderland</h1>
<h2>By <cite>Lewis Carroll</cite></h2>
</hgroup>
</header>
<article>
<h2>Chapter III</h2>
<span class="chaptertitle">A Caucus-race and a Long Tale</span>
<p>
They were indeed a queer-looking party that assembled on the bank&amp;mdash;the birds with draggled feathers,the animals with their fur clinging close to them, and all dripping wet, cross, and uncomfortable.</p>
<footer>
<a href="AAML-ch02">Chapter II - The Pool of Tears</a>
<a href=".../index.html">Table of Contents</a>
<a href="AAML-ch04">Chapter IV - The Rabbit sends in a Little Bill</a> &raquo;
</footer>
</body>
</html>
```

### Choosing Color Values

You can define colors in a variety of ways in CSS. Several methods simply represent how the primary colors—red, green, and blue—should be mixed, but that is by no means the only way colors are defined in CSS (Table 7.1).

### Color keywords

You have access to many predefined color values derived from lists defined in the HTML4 and SVG specifications. Table 7.2 shows the list of keywords along with the equivalent hex and decimal values.

TABLE 7.1 Color Values

| Name | Form | Example |
|---|---|---|
| Keyword | <keyword> | coral |
| Transparent | transparent | transparent |
| Current color | currentcolor | currentcolor |
| RGB hex | #rrggbb, #rgb | #ff7f50, #f90 |
| RGB decimal | rgb(rrr,ggg,bbb) | rgb(255,127,80) |
| RGB percentage | rgb(rrr%,ggg%,bbb%) | rgb(100%, 50%,31%) |
| RGBA | rgba(rrr,ggg,bbb,d) | rgba(255,127,80,.86) |
| HSL | hsl(hhh,sss%,lll%) | hsl(16,65%,100%) |
| HSLA | hsla(hhh,sss%,lll%,d) | hsla(16,65%,100%, 23) |
