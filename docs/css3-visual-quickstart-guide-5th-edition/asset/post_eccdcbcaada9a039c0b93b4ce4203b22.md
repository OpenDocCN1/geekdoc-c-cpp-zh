
Kerning—Remember that letter spacing is not kerning. The new punctuation-trim property will provide some rudimentary kerning capabilities.

Hanging Punctuation—One common problem in typography is what to do when alphanumeric characters are not present at the beginning of a block of text, as with quotation marks. The hanging-punctuation property will allow you to define how these characters are treated, either placing them in the text block or outside the edge of the block.

Text Line Decoration—As mentioned in my explanation of the text-decoration property, several new associated properties are being developed to style the text decoration, including text-line-color, text-line-style, text-line-skip, and text-underline-position.

To follow the development of these styles, visit the CSS3 Text Module at www.w3.org/TR/css3-text.

# Putting It All Together

- 1. Add letter, word, and line spacing to your headers. Try out different effects, pushing the text together and moving apart.
- 2. Add line spacing to your body copy. Specify the line height in paragraph elements. See how increasing and decreasing the space improves or reduces readability. At what point does increasing the line height reduce readability?
- 3. Set the text case of your headline to uppercase. You can also play with the font size to make the headlines stand out.
- 4. Add a text shadow to your headlines. Try to keep them subtle and not distracting.
- 5. Fully justify your body copy. Use justify alignment on the paragraph tag. Does this look better or worse than the ragged edges you get with left?
- 6. Indent your text paragraphs. Play around with different amounts of indentation and see what you prefer.

# Color and Background Properties

Colors form the cornerstone of all design, even if they only black and white. Bright, vibrant, jewel-like colors make a radically different statement than earth tones. Even if you choose only black and white, your design will make a state. Beyond decorative impact, colors can also guide the viewer's eye around the page, helping to highlight important areas while downplaying others. In this chapter, you will learn the primary methods used to add and control color. Keep in mind, however, you can specify using several properties. But before you learn how to code, quickly explore how to choose them.

# In This Chapter

- Choosing Color Values
- New in CSS3: Gradients in Backgrounds
- Choosing Your Palette
- Setting Text Color
- Setting a Background Image
- Using Shorthand
- Putting It All Together

The HTML5 code used for the examples in this chapter imports the final code from Chapters 5 and 6, and a new file named color-properties.css, which for this, we'll be styling Chapter 3 of Alice's Adventures in Wonderland, including a navigational footer at the bottom.

```html
<!DOCTYPE html>
<html lang="utf-8">
<head>
<meta charset="utf-8">
<title>Alice's Adventure in Wonderland</title>
<link href="../font-properties.css" type="text/css" rel="stylesheet">
<link href="../css/text-properties.css" type="text/css" rel="stylesheet">
<link href="../css/color-background-properties.css" type="text/css" rel="stylesheet">
<!--[if IE]-->
<style>@import url(css/ie.css);</style
<script src="HTML5.js" type="javascript"></script>
<!--[endif]-->
</head>
<body id="chapter3" class="body">
<header class="page">
<h1>Alice's Adventures In Wonderland</h1>
<p class="byline">by Alice Carroll</p>
</header>
<article>
<header>
<h2><strong>CHAPTER III.</strong> A Caucus-Race and a Long Tale</h2>
</header>
<p>They were indeed a queer-looking party that assembled on the bank—the birds with dragged feathers, the animals with their clinging to them, and all dripping wet, cross, and uncomfortable.</p>
</article>
<footer>
<ul>
<li><a href="#">Table of Contents</a></li>
<li><a href="#">About the Author</a></li>
<li><a href="#">About the Books</a></li>
<li><a href="#">About the Site</a></li>
</ul>
</footer>
</body>
</html>
```

# Choosing Color Values

The saying, "There is more than one way to skin a cat," is grotesque, but it is also applicable to most creative decisions, such as color values in Web designs. You can use several traditional methods to define the same Web page color, and CSS3 even introduces a few ways.

# Color keywords

Although most designers have little use for predefined colors, you have access to many predefined color values derived from lists defined in the HTML4 and SVG specifications. Table 7.1 shows the list of keywords along with the equivalent hex and decimal values. Values in boldface indicate inclusion from HTML

| TABLE 7.1 Color Values | Name | Form | Compatibility |
| :--- | :--- | :--- | :--- |
| Keyword | <keyword> | coral | IE4, FF1, S1, C1, O3.5, CSS1 |
| Transparent | transparent | - | IE4, FF1, S1, C1, O3.5, CSS1 |
| Current color | currentColor | - | FF3.6, S2, C2, O10, CSS3 |
| RGB hex | #rrr,ggg,bbb | #ff71f5, #f190 | IE4, FF1, S1, C1, O3.5, CSS1 |
| RGB decimal | rgb(rrr,ggg,bbb) | 255,127,80 | IE4, FF1, S1, C1, O3.5, CSS1 |
| RGB percentage | rgb(rrr%%,ggg%%,bbb%%) | rgb(100%,50%,31%) | IE4, FF1, S1, C1, O3.5, CSS1 |
| HSL | hsla(hhh,sss,lll%) | hsla(16,65,100%) | IE4, FF1, S1, C1, O3.5, CSS1 |
| RGBA | rgba(rrr,ggg,bbb,a) | rgba(255,127,80,1) | IE4, FF1, S1, C1, O3.5, CSS1 |
