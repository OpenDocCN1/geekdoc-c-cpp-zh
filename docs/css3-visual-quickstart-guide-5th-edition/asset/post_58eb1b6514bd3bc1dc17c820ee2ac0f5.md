
## NEW IN CSS3:
Querying the Media ★

| TABLE 4.7 Media Values |
| Value | Intended for |
| --- | --- |
| screen | Computer displays |
| tty | Teletypes, computer terminals, and older portable devices |
| tv | Television displays |
| projection | Projectors |
| handheld | Portable phones and PDAs |
| print | Paper |
| braille | Braille tactile readers |
| speech | Speech synthesizers |
| all | All devices |

In Chapter 3 you learned how to specify style sheets for a particular media type, allowing you to set styles depending on whether the HTML is output to a screen, print, TV, or a handheld or other device (Table 4.7). CSS adds an important new capability that allows you to set styles based on common interface properties such as width, height, aspect ratio, and number of available colors.

Media queries and the @media rule can be used to tailor your page, not just to a generic device type but to the specific device your visitor is. This includes sizing for print, for mobile devices, or to best fit the size of the open browser window.

```
@media screen
and (min-width: 600px)
and (max-width: 980px)
```

## Media queries

If you want to know the current size of the browser window, why not just ask the browser? JavaScript gives you the ability to do this, but it's a cumbersome way to get some basic facts about the Webbed environment your design is trying to fit into.

Media queries provide you with several common media properties that you can test and then delivers the style sheet that best suits your environment.

Although media queries have many proper properties (Table 4.8), they come in five basic flavors:

- Aspect-ratio looks for the relative dimensions of the device expressed as a ratio: 16:9, for example.
- Width and height looks for the dimensions of the display area. These can also be expressed as maximum values.

> The general syntax for media queries.

## TABLE 4.8 Media Query Properties

| Property | Value | Compatibility |
| --- | --- | --- |
| aspect-ratio | <ratio> | FF3.5, S1, O9.5, CSS3 |
| max-aspect-ratio | <ratio> | FF3.5, S1, O9.5, CSS3 |
| min-aspect-ratio | <ratio> | FF3.5, S1, O9.5, CSS3 |
| device-aspect-ratio | <ratio> | FF3.5, S1, O9.5, CSS3 |
| max-device-aspect-ratio | <ratio> | FF3.5, S1, O9.5, CSS3 |
| min-device-aspect-ratio | <ratio> | FF3.5, S1, O9.5, CSS3 |
| color | <integer> | FF3.5, S1, O10, CSS3 |
| max-color | <integer> | FF3.5, S1, O10, CSS3 |
| min-color | <integer> | FF3.5, S1, O10, CSS3 |
| color-index | <integer> | FF3.5, S1, O10, CSS3 |
| max-color-index | <integer> | FF3.5, S1, O10, CSS3 |
| min-color-index | <integer> | FF3.5, S1, O10, CSS3 |
| device-height | <length> | FF3.5, S1, O9.5, CSS3 |
| max-device-height | <length> | FF3.5, S1, O9.5, CSS3 |
| min-device-height | <length> | FF3.5, S1, O9.5, CSS3 |
| device-width | <length> | FF3.5, S1, O9.5, CSS3 |
| max-device-width | <length> | FF3.5, S1, O9.5, CSS3 |
| min-device-width | <length> | FF3.5, S1, O9.5, CSS3 |
| height | <length> | FF3.5, S1, O9.5, CSS3 |
| max-height | <length> | FF3.5, S1, O9.5, CSS3 |
| min-height | <length> | FF3.5, S1, O9.5, CSS3 |
| monochrome | <integer> | FF3.5, S1, O10, CSS3 |
| max-monochrome | <integer> | FF3.5, S1, O10, CSS3 |
| min-monochrome | <integer> | FF3.5, S1, O10, CSS3 |
| orientation | portrait, landscape | FF3.5, S1, C1, CSS3 |
| resolution | <resolution> | FF3.5, S1, O10, CSS3 |
| max-resolution | <resolution> | FF3.5, S1, O10, CSS3 |
| min-resolution | <resolution> | FF3.5, S1, O10, CSS3 |
| scan | progressive, interlaced | FF3.5, S1, O10, CSS3 |
| width | <length> | FF3.5, S1, O9.5, CSS3 |
| max-width | <length> | FF3.5, S1, O9.5, CSS3 |
| min-width | <length> | FF3.5, S1, O9.5, CSS3 |

- Orientation looks for landscape (height greater than width) or portrait (width greater height) layout. This allows you to tailor designs for devices that can flip.
- Color-index and monochrome finds the number of colors or bits per color. These allow you to tailor design for black and white devices.
- Resolution looks at the density of pixels in the output. This is especially useful when you want to take advantage of displays that have a higher resolution than 72 dpi.

By default, media queries are for viewport (see Chapter 11 for details) on exception of those that specify device, in which case they are for the entire screen or output area. For example, width is the width of the visible viewport, whereas device-width is the width of the entire screen.

Using media queries to specify:

- 1. Create a default style sheet that captures all the general styles for your design and save it (Code 4.14) default.css—These styles are applied regardless of the media type and include sans-serif fonts, a dark background, and light text.
- 2. Create style sheets for the various media or specific devices such as the iPhone (Code 4.15) print.css—These styles are tailored for the printed page, changing the background to white (using paper), serif fonts, black text, and a different background image to match.
- 3. Add the viewport meta tag. In the head of your HTML document (Code 4.17), add a meta tag with a name equal to viewport and content, as shown.

```html
<meta name="viewport"
  content="width=device-width;
  initial-scale=1.0;
  maximum-scale=1.0;
  user-scalable=0;">
```

This will prevent devices with smaller screens, most notably the iPhone, from overriding your styles to be set in step 5.

![](img/9cd61ac1d4015ed5688d0c411434a660_127_0.png)

## Alice's Adventures in Wonderland
By Lewis Carroll

Chapter 1. Down the Rabbit-Hole

Alice was beginning to get very tired of sitting by her sister, and of having nothing to do; she began at the book her sister was reading, which had no pictures or words. “And what,” thought Alice, “what is the use of a book without pictures or conversations?"

- Code 4.17 output to a computer screen. This version uses a dark background and an inverted version of the Alice's Adventures in Wonderland illustration. On an LCD screen, the lightly colored text will look fine.

Code 4.17 The HTML code links to all three of the style sheets, which are displayed in B, C, and D.

```css
*** Default Styles ***
body {
  background: black url('../images/alice.gif') no-repeat 0;
  margin: 0;
  padding: 200px 175px;
}
h1 {
  color: white;
  font-style: italic;
}
h2 {
  color: rgb(153,153,153);
}
p {
  font: normal 100% / Helvetica, Arial, Sans-serif;
  color: rgb(204,204,204);
}
```

```css
*** For Print ***
body {
  background: white url('../images/alice.gif') no-repeat 0;
  padding: 200px 0 175px;
}
h1 {
  color: black;
}
p {
  font: normal 12pt / Constantia, palatino, "times new roman", serif;
  color: rgb(0,0,0);
}
```

```css
*** iPhone Styles ***
body {
  -webkit-text-size-adjust:none;
  background: rgb(102,102,102) url('../images/alice.gif') no-repeat
  center: 0;
  padding: 120px 20px 20px;
}
h1 {
  color: rgb(153,125,125);
  text-shadow: 0 0 5px rgb(0,0,0);
}
p {
  font: normal 1em / 1.25em "helvetica neue", Helvetica, Arial, Sans-serif;
  color: rgb(255,255,255);
}
```
