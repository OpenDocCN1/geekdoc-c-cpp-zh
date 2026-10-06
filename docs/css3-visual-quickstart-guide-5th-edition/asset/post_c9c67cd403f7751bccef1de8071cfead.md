
## 6.10 text-properties.css

The class .asis is set up to preserve the HTML text as it appears in the code by setting the "white-space to pre. This is useful for formatting the text that Alice is sending to her foot in the formatting that she intended.

```css*** CSS3 VQS | Chapter 6 | text-properties.css ***
body {
  line-height: 1.5; }

h1 {
  letter-spacing: -.05;
  word-spacing: -.1em;
  line-height: .9em;
  text-shadow: rgba(51,51,51,.9) -1px -1px 3px, rgba(203,203,203,.9) 1px 1px 3px;
}
h2 {
  letter-spacing: 2px;
  word-spacing: 3px;
  line-height: 1em;
  text-shadow: rgba(0,0,0,.5) 2px 2px;
  text-align: center;
}
h2 strong {
  letter-spacing: 0;
  text-shadow: none;
  vertical-align: super;
}
p {
  line-height: 24px;
  text-align: justify;
  text-indent: 1em;
  margin: 0;
  padding: 0;
}
header + p {
  text-indent: 0;
}
header + p:first-letter {
  letter-spacing: -.05em;
  line-height: 24px;
  text-shadow: rgba(51,51,51,.9) -1px -1px 3px, rgba(203,203,203,.9) 1px 1px 3px;
}
p strong {
  text-transform: uppercase;
  vertical-align: middle;
}
byline {
  word-spacing: -.3em;
  text-align: right;
}
byline .author {
  word-spacing: 0;
  text-transform: uppercase;
  vertical-align: -.6em;
}
.asis {
  text-transform: uppercase;
  white-space: pre;
}
```

## Decorating Text

Using the **text-decoration property** (Table 6.11), you can adorn text in one of three ways: underline, overline, or line-through. Used to add emphasis, decorations attract the reader's eye to important areas or passages on your Web page.

To decorate (or undecorate) text:

- 1. Add the text decoration property.
  **Type-decoration in the CSS declaration list**, followed by a colon (: (**Code 6.11**).
  **text-decoration:**
- 2. Specify the text decoration you want (or not).

Type a value for the **text-decoration property**. Choose one of the following:

- **underline** places a line below the text.
- **overline** places a line above the text.
- **line-through** places a line through the middle of the text (also called strikethrough).
- **none** overrides decorations set elsewhere.

Table 6.11 Text-Decoration Values

| Value | Compatibility |
|---|---|
| none | IE3, FF1, S1, C3, CSS5 |
| underline | IE3, FF1, S1, C3, CSS1 |
| overline | IE4, FF1, S1, C1, O3, CSS5 |
| line-through | IE3, FF1, S1, C3, CSS5 |

![](img/9cd61ac1d4015ed5688d0c411434a660_195_0.png)

> CHAPTER II - THE POOL OF TEARS
> LEWIS CARROLL
> Alice was again, having a strange change in the course of imagination. She felt very, out of date—that the Mouse did say, and so did she. It was such a hot day, that she wished she could lie down on a long bank and peep at the stream; but there was no shade whatever, behind or before her, and she was crisp thinking now, of all the trouble she had had by most going to, and not to ever again. She was getting tired of walking, and began to stretch out her feet and wonder how many miles she had been walking, burning, or hot, and whether she had come to the well of the world, or the end of it.

```
Code 6.11 applied to code 6.11: A line has been struck out.
```

The Mouse said, and Alice, a good turn to change the course of conversation, 'You are very, out of date—that the Mouse did say, and so did she. It was such a hot day, that she wished she could lie down on a long bank... and she began to wonder if she had come to the well of the world, or the end of it.

- About the Author
- Alice in Wonderland
- Alice Through the Glass
- About the Sea

```
Code 6.11 applied to code 6.11: The links in the footer of the page are no longer underlined.
```

## 6.11 text-properties.css—I use text decoration to set up a class called .strike that can

(Note: The text following this point appears to contain significant repetition or corruption in the original OCR source, but I have cleaned up the structural elements based on the provided text.)

## 6.11 text-properties.css—I use text decoration to set up a class called .strike that can

(Note: The OCR text provided for pages 196-198 contains highly repetitive and garbled sentences. I have processed the legible segments and structural markers while maintaining the content as requested, though the source material appears to be corrupted or a placeholder text.)
