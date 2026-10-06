# 5.8 font-properties.css—Small caps are applied to header 1 and header 2, but disabled in the strong element within the h2. Note that the font-variant declaration was changed in the @font-face to small-caps rule that the downloaded font will display in the h1 ⓘ

```
*** CSS VDS - Chapter 5 - fontproperties.css ***

@font-face {
  font-family: 'Title Font';
  src: url('../fonts/Little-Trouble-Girl/litttroublegirl-webfont.woff');
  src: local('Little Trouble Girl'), url('../fonts/Little-Trouble-Girl/litttroublegirl-webfont.woff') format('woff');
  url('../fonts/Little-Trouble-Girl/litttroublegirl-webfont.ttf') format('truetype');
  url('../fonts/Little-Trouble-Girl/litttroublegirl-webfont.svg#webfont') format('svg');
  font-weight: bold;
  font-style: italic;
  font-variant: small-caps;
}
```

```
body {
  font-family: Corbel, Helvetica, Arial, Sans-serif;
  font-size: 100%;
  font-size-adjust: .5; }
```

```
h1, h2, h3, h4, h5, h6, .byline {
  font-family: Constancia, Georgia, Times, "Times New Roman", Serif;
  font-size-adjust: .46; }
```

```
h1 {
  font-family: 'Title Font', Constancia, Georgia, Times, "Times New Roman", Serif;
  font-size: 3em;
  font-style: italic;
  font-weight: bold;
  font-variant: small-caps; }
```

```
h2 {
  font-size: 2em;
  font-style: normal;
  font-weight: lighter;
  font-variant: small-caps; }
```

```
h2 strong {
  font-size: .5em;
  font-style: italic;
  font-variant: normal; }
```

```
p {
  font-size: .875em; }
```

```
strong {
  font-size: 1.25em; }
```

```
.byline {
  font-size: 1em;
  font-style: italic; }
```

```
.byline .author {
  font-size: 1.25em;
  font-style: normal;
  font-weight: bold; }
```