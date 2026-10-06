
Code 5.6 font-properties.css—The h1 and h2 tags both have italic for them, this being overridden the strong tag with an h2. We also need to change the font-style in the @font-face rule. This does not actually italicize the downloaded font, it tells the browser to use this in place of italicized version.

```css
*** VQS - Chapter 5 - font-properties.css ***
@font-face {
  font-family: 'Title Font';
  src: url('./fonts/little-Trouble-Girl/littletoublegirl-webfont.eot');
  src: local('Open Sans'), url('./fonts/little-Trouble-Girl/littletoublegirl-webfont.woff') format('woff'),
  url: url('./fonts/little-Trouble-Girl/littletoublegirl-webfont.ttf') format('truetype');
  url: url('./fonts/little-Trouble-Girl/littletoublegirl-webfont.svg#svg') format('svg');
  font-weight: normal;
  font-style: italic;
  font-variant: normal;
}

body {
  font-family: Corbel, Helvetica, Arial, Sans-serif;
  font-size: 100%;
  font-size-adjust: .5;
}

h1, h2, h3, h4, h5, h6, .byeline {
  font-family: Constantia, Georgia, Times, "Times New Roman", Serif;
  font-size-adjust: .46;
}

h1 {
  font-family: 'Title Font', Constantia, Georgia, Times, "Times New Roman", Serif;
  font-size: 3em;
  font-style: italic;
}

h2 {
  font-size: 2em;
  font-style: normal;
}

h2 strong {
  font-size: .5em;
  font-style: italic;
}

p {
  font-size: .85em;
}

strong {
  font-size: 1.25em;
}

.byeline {
  font-size: 1.25em;
  font-style: italic;
}

.byeline .author {
  font-style: normal;
}
```

TIP Many browsers do not differentiate between italic and oblique; will simply use the fonts italic version (if available), even when they are set to oblique.

TIP If an italicized or oblique version of the typeface does not exist, many browsers will attempt to synthesize one by slanted the normal version of the font to the right. This rarely looks good and should be avoided.

TIP Many Web designers underline words to draw visual attention to them. I recommend using italic or oblique text instead. Underlining often causes the page to look cluttered. More important, underlined text might be confused with hypertext links.

TIP Italicized text generally fits into a more compact space than non-italic text (called roman in traditional typesetting terms) and could be used to save screen space. But could be careful—at small point sizes, italic can be difficult to read on the screen.

# Alice's Adventures In Wonderland

by Lewis Carroll

## Chapter 1. Down the Rabbit-Hole

Alice was beginning to get very tired of sitting by her sister on the bank, and of having nothing to do: once or twice she had peeked into the book her sister was reading, but it had no pictures or conversations in it, 'and what is the use of a book,' thought Alice 'without pictures or conversation?'

So she was considering in her own mind (as well as she could, for the hot day made her feel sleepy and stupid), whether the pleasure of making a daisy-chain would worth the trouble of getting up and picking the daisies, suddenly, a White Rabbit with pink eyes ran close by her.

There was nothing so remarkable in that; nor did Alice think it was so very much out of the day to hear the Rabbit say to itself, 'Oh dear! Oh dear! I shall be late!' (when she thought it over afterwards, it occurred to her that she ought to have wondered this, but at the time it all seemed quite natural); but when the Rabbit actually took a watch out of its waistcoat-pocket, and looked at it, and then hurried on, Alice started to her feet, for it flashed across her mind that

> Italics are often used to help set off text, such as with the word 'by,' or to add emphasis, as with the chapter title.

# Setting Bold, Bolder, Boldest

# normal bold

CSS provides several options that allow you to set different levels of boldness for text. Many fonts have various weights associated with them; these weights have the effect of making the text look more or less bold (Table 5.7). CSS can take advantage of this feature.

A The difference between normal and bold text is evident here.

| TABLE 5.7 Font-Weight Values |
| Value | Compatibility |
| --- | --- |
| normal | IE3, FF1, S1, C1, O5, CSS1 |
| bold | IE3, FF1, S1, C1, O5, CSS1 |
| lighter | IE4, FF1, S1 |
| bolder | IE4, FF1, S1, C1, O5, CSS1 |
| 100-900* | IE4, FF1, S1, C1, O5, CSS1 |

# To define bold in a CSS rule:

- 1. Add the font weight property.
- 2. Define the font weight:
```css
font-weight: bold;
```
- 3. Use numeric values (100-900):
```css
font-weight: 400;
```
- 4. Use keyword values:
```css
font-weight: lighter;
```
- 5. Use relative values:
```css
font-weight: bolder;
```
