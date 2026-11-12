
## normal italic oblique

A Italic or oblique? To really tell the difference, take a careful look at the letter “T” in both words.

### TABLE 5.8 Font-Style Values

| Value | |
|---|---|
| normal | |
| italic | |
| oblique | |

Code 5.6 Styles added to font-properties.css— The h1 and h2 tags both have italic set for them with this being overridden in the strong tag within an h2 ➋. We also need to change the font-style in the @font-face rule. This does not actually italicize the downloaded font, it just tells the browser to use this in place of an italicized version.

```
h1 { font-style: italic; }
h2 { font-style: normal; }
h2 cite { font-style: italic; }
figcaption { font-style: italic; }
```

![](img/e1ed1e3c1873fa9fc855210fb83699d0_168_0.png)

B Italics are often used to help set off text or to add emphasis, as with the chapter title.

## Making Text Italic

Two kinds of styled text that are often confused are italic and oblique. An italic font is a special version of a particular font, redesigned with more pronounced serifs and usually a slight slant to the right. An oblique font, on the other hand, is simply a font that is slanted to the right but otherwise identical to the normal version.

Using the font-style property (Table 5.8), you can define a font as italic, oblique, or normal. When a font is set to italic but does not have an explicit italic version, the font defaults to oblique A

## To set font-style for an element:

- 1. Add the font-style property to your CSS. Type the property name font-style (Code 5.6), followed by a colon (:).
  font-style: italic;

- 2. Define a style value. Type a value for the font-style. Your options are:
  - italic, which displays the type in an italic version of the font
  - oblique, which slants the text to the right
  - normal, which overrides any other styles set

```
h2 strong { font-style: normal; }
```

- 3. Add style overrides as needed. You can override italics or oblique by setting the font style for a child element to normal.

Many browsers do not differentiate between italic and oblique but will simply use the fonts' italic version (if available), even when they are set to oblique.

> TIP If an italicized or oblique version of the typeface does not exist, many browsers will attempt to synthesize one by slanting the normal version of the font to the right. This rarely looks good and should be avoided.

> TIP Many Web designers underline words to draw visual attention to them. I recommend using italic or oblique text instead. Underlining often causes the page to look cluttered. More important, underlined text might be confused with hypertext links.

> TIP Italicized text generally fits into a more compact space than non-italic text (called roman in traditional typesetting terms) and could be used to save screen space. But be careful—at small point sizes, italic can be difficult to read on the screen.

## normal bold

A The difference between normal and bold text is evident here.

| Value | |
|---|---|
| normal | ● ● ● ● ● ● |
| bold | ● ● ● ● ● ● |
| lighter | ● ● ● ● ● ● |
| bolder | ● ● ● ● ● ● |
| 100-900* | ● ● ● ● ● ● |

* Depending on available font weights

Code 5.7 font-properties.css—The author's name is bold to make it stand out B.

```
.byline .author {
  font-weight: bold;
}
```

![](img/e1ed1e3c1873fa9fc855210fb83699d0_170_0.png)

B The author's name is bold to stand out.

## Font-Weight Numbers

Most fonts do not have nine weights, so if the specified weight is not available, another weight is used:

- 100 to 300 lighter or darker.
- 400 and 500 normal.
- 600 to 900 use the next darker weight, if available, or the next lighter weight.

## Setting Bold, Bolder, Boldest

CSS provides several options that allow you to set different levels of boldness for text. Many fonts have various weights associated with them; these weights have the effect of making the text look more or less bold (Table 5.9). CSS can take advantage of this feature A.

## To define bold text in a CSS rule:

- 1. Add the font-weight property to your CSS. Type the property name font-weight (Code 5.7), followed by a colon (:).
  font-weight:

- 2. Define the weight.
  bold;
  Type the value for the font-weight property, using one of the following options:
  - bold, which sets the font to boldface
  - bolder or lighter, which sets the font's weight to be bolder or lighter relative to its parent element's weight
  - A value from 100 to 900, in increments of 100, which increases the weight, based on alternative versions of the font that are available
  - normal, which overrides other weight specifications

> TIP Use font-weight to add emphasis to text, but use it sparingly. If everything is bold, nothing stands out.

> TIP In reality, most fonts support only normal and bold, so relative values have an absolute effect

## Using Condensed and Expanded Fonts

Although the bold and italic versions of fonts are most common, many fonts have versions that are condensed (narrower) or extended (wider) ➊. The font-stretch property allows you to reference particular font widths (Table 5.10). Some fonts include font widths that stretch or compress the font and are different from bold, which simply makes the letterform consistently thicker. Most fonts will not have these properties, but for those that do, using font-stretch will be the best way to access them.

## To define condensed or extended fonts in a CSS rule:

- 1. Add the font-stretch property to your CSS. Type the property name font-stretch (Code 5.8), followed by a colon (:).
  font-stretch:

- 2. Define the weight.
  condensed;
  Type the value for the font-stretch property, using one of the following options:
  - A value from Table 5.10.
  - normal, which overrides other weight specifications

## normal condensed expanded

![](img/e1ed1e3c1873fa9fc855210fb83699d0_171_0.png)

| Value | |
|---|---|
| ultra-condensed | ➊➋ |
| extra-condensed | ➊➋ |
| condensed | ➊➋ |
| semi-condensed | ➊➋ |
| semi-expanded | ➊➋ |
| expanded | ➊➋ |
| extra-expanded | ➊➋ |
| ultra-expanded | ➊➋ |
| normal | ➊➋ |
| inherit | ➊➋ |

Code 5.8 Added to font-properties.css—The author's name is set in condensed text ➋

```
h2 cite { font-stretch: condensed; }
```

![](img/e1ed1e3c1873fa9fc855210fb83699d0_171_1.png)

The author's name is condensed. ➋

## Normal SMALLCAPS

With small caps, all the letters are uppercase, but the first letter is larger than the others.

| Value | |
|---|---|
| normal | |
| small-caps | |

Code 5.9. Styles added to font-properties.css— Small caps are applied to both header 1 and header 2, but disabled in the strong element within the h2. Note that the font-variant declaration was changed in the @font-face to small-caps rule so that the downloaded font will display in the h1.

```
h1 { font-variant: small-caps; }
h2 { font-variant: small-caps; }
```

![](img/e1ed1e3c1873fa9fc855210fb83699d0_172_0.png)

Using small caps for the title is an elegant way to set it off from the rest of the text.

## Creating Small Caps

Small caps (sometimes referred to as mini-caps) are useful for emphasizing titles (Table 5.11). With small caps, lowercase letters are converted to uppercase but in a slightly smaller size than regular uppercase letters

## To set small caps for an element:

- 1. Add the font-variant property to your CSS. Type the property name font-variant (Code 5.9), followed by a colon (:). font-variant:

- 2. Define a value for the variant. small-caps; Type the value of the font-variant property, using one of the following options:
  - small-caps, which sets lowercase letters as smaller versions of true uppercase letters
  - normal, which overrides other font-variant values that might be inherited

> TIP Small caps are best reserved for titles or other special text; they can be hard to read at smaller sizes.
