5.5 font-properties.css—The font size has been adjusted so that lowercase letters are half the size of uppercase letters 0. An exception is with the header font, where the font size is set at .46 C

```
*** CSS VQS - Chapter 5 - font-properties.css ***
@font-face {
  font-family: 'Title Font';
  src: local('../fonts/Little-Trouble-Girl/littleretroublegirl-webfont.wot');
  src: local('\02'), url('../fonts/Little-Trouble-Girl/littleretroublegirl-webfont.woff') format('woff');
  url('../fonts/Little-Trouble-Girl/littleretroublegirl-webfont.ttf') format('truetype');
  url('../fonts/Little-Trouble-Girl/littleretroublegirl-webfont.svg#webfont') format('svg');
  font-weight: normal;
  font-style: italic;
  font-variant: normal;
}

body {
  font-family: Helvetica, Arial, Sans-serif;
  font-size: 100%;
  font-size-adjust: .5; 
}

h1, h2, h3, h4, h5, h6, .byline {
  font-family: Georgia, Times, "Times Roman", Serif;
  font-size-adjust: .46;
}

h1 {
  font-family: Constantia, Georgia, Times, "Times New Roman", Serif;
  font-size: 3em;
}

h2 {
  font-size: 2em;
}

h2 strong {
  font-size: .5em;
}

p {
  font-size: .875em;
}

strong {
  font-size: 1.25em;
}

byline {
  font-size: 1.25em;
}

byline.author {
```