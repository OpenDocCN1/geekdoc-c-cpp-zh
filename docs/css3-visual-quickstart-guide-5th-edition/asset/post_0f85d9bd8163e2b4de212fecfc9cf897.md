
![](img/9cd61ac1d4015ed5688d0c411434a660_128_0.png)

## 3. Link to your default style sheet. In the head of your HTML document, type a <link> tag that references the default version of the CSS and define media as all.

```html
<link rel="stylesheet" href="default.css">
```

## 4. Link to your print style. Immediately after the <link> tag, add another <link> that references the print version of the CSS and define media as print.

```html
<link rel="stylesheet" href="print.css">
```

## 5. Use a media query to link to a style sheet. Immediately after the previous <link> tag, add another <link> tag that references the style sheet for a specific media type and add media queries (Table 4.8) in parentheses connecting multiple queries with and.

```html
<link rel="stylesheet" media="screen and (max-device-width: 320px)" and href="iphone.css">
```### Alice’s Adventures In Wonderland

by Lewis Carroll

## Chapter I. Down the Rabbit-Hole

Alice was getting very tired of sitting on the bank, and beginning to do sleepy, that if she had gone into the rabbit hole she was staring at; there were no pictures or conversations going on, and what was the use of a book, without pictures or conversations?

She was also curious as to how (as well as she could, for the hot made her very sleepy) and whether the pleasure of making a strange wish would be worth the trouble of going after it, especially when the White Rabbit with pink eyes ran right by her.

There was no time to thank or slip, nor was there much of the way to catch the Rabbit to say goodbye; but she fell down down, down, down, wondering how long she would reach the bottom of the well.

![](img/9cd61ac1d4015ed5688d0c411434a660_128_1.png)

## Code 4.17 on an iPhone

A specially tailored version to fit the width of an iPhone uses a custom header of Cheshire cat.

> TIP Before media queries were introduced, Web developers used JavaScript to detect browser dimensions and colors. Media queries render these techniques obsolete, at least for styling purposes.

> TIP In this example, media queries are applied to the media property value of the <link> tag, but you can as easily apply them to the media property of the <style> tag.

Selective Styling 105

## Using the @media rule

Media queries allow you to specify styles in the media property of <link> and <style> tags, but the @media rule allows you to embed media queries directly into a style.

### Using @media to specify styles:

- 1. Create your style sheets. Create an external style sheet or embed a style sheet in the body of your document (Code 4.18).
- 2. Use the @media rule to specify styles with media queries. In the head of your HTML document, type @media and media. Then specify the media type (Table 4.7) and any media queries (Table 4.8) for the styles.

```css
@media screen (max-device-width: 480px) and (min-device-width: 320px) {...}
```

For example, you might specify that these styles are correct with a width between 320px and 480px. Finish with curly brackets. Add any media-specific styles between the curly brackets.

- 3. Add other styles as necessary. {...}

```css
h2 string {...}
```

You can add @media rules or other nonmedia-specific rules. However, all CSS rules that are not in @media, @font-face, and import, and so on must come after the rules.

- 4. Link to the style sheet from your HTML document. Place a link tag to add the external CSS file (Code 4.19).

TIP Remember that @media rules can go in external or embedded style sheets.

```css
/* The general syntax of the @media */
@media screen and (width=480px) {
  h1 { color: red; }
}
/* CSS rules */
/* Code 4.18 screen.css--The iPhone code from 4.15 has been combined with more generic CSS. */

*** Screen Styles ***
@media screen and (max-device-width: 480px) and (min-device-width: 320px) {
  body {
    -webkit-text-size-adjust:none;
    background: rgb(102,102,102) url('../images/alpha.gif') no-repeat center;
    padding: 20px 20px 20px;
  }
  h1 {
    color: rgb(153,125,125);
    text-shadow: 0 0 1px rgba(0,0,0);
    font: normal 1em/1.25em "helvetica", Arial, Sans-serif;
  }
  h2 string {
    display: block;
    color: red;
    font-size: .75em;
    font-style: italic;
  }
}

/* iPhone Styles ***
@media screen and (max-device-width: 480px) and (min-device-width: 320px) {
  body {
    color: rgb(255,255,255);
  }
}
```

## 4.19 The HTML code links to the various style sheets for different media types. The big difference between this and before is that the iPhone-specific code is now embedded in screen, not including media queries.

```html
<!-- HTML -->
<!DOCTYPE html>
<html lang="en">
<head>
  <meta http-equiv="Content-Type" content="text/html; charset=UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Alice's Adventures in Wonderland</title>
  <link rel="stylesheet" media="all" href="default.css">
  <link rel="stylesheet" media="print" href="print.css">
  <link rel="stylesheet" media="screen" href="screen.css">
</head>
<body>
  <h1>Alice's Adventures in Wonderland</h1>
  <p class="byline">by <span class="author">Lewis Carroll</span></p>
  <article>
    <header>
      <h2><strong>Chapter I.</strong> Down the Rabbit Hole</h2>
    </header>
    <p>Alice was beginning to get tired of sitting by her sister...</p>
  </article>
</body>
</html>
```

Alice was beginning to get tired of sitting by her sister...![](img/9cd61ac1d4015ed5688d0c411434a660_130_0.png) Code 4.18 on an iPhone. This looks the same, but the code is now in an @media rule.

## Styling for Print

With the advent of laser and inkjet printers, we seem to be buried under mounds of printed paper. Even the Web seems to have increased the amount of paper we use. If an article on the Web is longer than a couple of scrolls, many people print it.

But the Web was created to display information on the screen, not on paper. Web graphics look blocky when printed, and HTML lacks many layout controls. That said, you can take steps to improve the appearance of printed Web pages. Looking good in print and on the Web may take a little extra effort, but your audience will thank you in the long run.

Here are six simple things you can do to improve the appearance of your Web when it is printed:

- Use breaks before page headers to keep them with their text.
- Separate content from navigation. To keep the main content—the part your audience is interested in reading—in a separate area of the design from the site navigation. You can then use CSS to hide navigation in the printed version with:

```css
nav { display: none }
```
included in the print style sheet.
- Avoid using transparent colors in graphics. This is especially true if the graphic is on a background color other than white. The transparent area of a GIF image usually prints white regardless of the color behind it in the window. This situation is not a problem if the graphic is on a white background to begin with, but the result is messy if the graphic is supposed to be on a dark background.
- Avoid using text in graphics. The irony of printing content from the Web is that text in graphics, which may look smooth in the window can look blocky when printed; but regular HTML text, which may look blocky on some PC screens, can print smoothly on any decent printer. Try to stick with HTML text as much as possible.
- Avoid dark-colored backgrounds and light-colored text. Generally you want to keep white as your background color for the printed page, and black or dark gray for the text.
- Do not rely on color to convey your message when printed. Although color printers are quite common these days, many people are still printing with black-and-white printers or printing in black and white on color printers to save money.

## Inheriting Properties from a Parent

No, this book hasn't suddenly become the Visual QuickStart Guide to Real Estate. Child and descendant HTML tags generally assume the styles of their parents—inherit them—whether the style is using CSS or is inherited from a browser style. This is called inheritance of styles.

For example, if you use an ID copy and give it a font-family value of Times, all of its descendants would inherit the Times font style. If you set a **bold** tag to red with CSS, all of its descendants will inherit both the applied bold style.

## CSS

```css
b { color : red; }
.copy { font-family: times; }
```

![](img/9cd61ac1d4015ed5688d0c411434a660_132_0.png)

## RESULT
Curiouser and curiouser!

The final result of the styles applied and inherited is bold, red, and italicized text in Times font.
