# Code 6 text-properties.css—Although you can indent any block of text. indentation is generally associated with paragraphs, and I set all of the paragraphs to indent 2em. However, the first paragraph in a section is generally not indented; however, I set the first paragraph after a header to always have an indentation of 0. I did a bit for this example, because I set the margin and padding, which we will not explore until Chapter 8.

*** CSS33 VQS | Chapter 6 | text-properties.css ***/

```
body {
  line-height: 1.5; }

h1 {
  letter-spacing: -.05em;
  word-spacing: -.1em;
  line-height: .9em;
  text-shadow: rgba(51,51,51,.9) -1px -1px 3px, rgba(203,203,203,.9) 1px 1px 3px; }

h2 {
  letter-spacing: 2px;
  word-spacing: 3px;
  line-height: 1em;
  text-shadow: rgba(0,0,0,.5) 2px 2px 2px;
  text-align: center; }

h2 strong {
  letter-spacing: 0;
  text-shadow: none;
  vertical-align: super; }

p {
  word-spacing: .07em;
  line-height: 24px;
  text-align: justify;
  text-indent: 2em;
  margin: 0;
  padding: 0; }

p strong {
  text-transform: uppercase;
  vertical-align: middle; }

header + p {
  text-indent: 0; }

header + p:first-letter {
  letter-spacing: -.05em;
  line-height: 24px;
  text-shadow: rgba(51,51,51,.9) -1px -1px 3px, rgba(203,203,203,.9) 1px 1px 3px; }

byline {
  word-spacing: -.3em;
  text-align: right; }

.byline {
  word-spacing: 0;
  text-transform: uppercase;
  line-height: .6em; }

asis {
  text-transform: uppercase; }
```