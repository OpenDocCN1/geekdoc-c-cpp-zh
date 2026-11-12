| Value | Icons |
|---|---|
| normal | ● ● ● ● ● ● |
| <length> | ● ● ● ● ● ● |

Code 6.3 Added to text-properties.css—When applied to Code 6.1, The words in the level 1 heading are spaced almost on top of each other, but this works because the words are visually separated by the capital letters. The words in the chapter title class are spaced out. The copy (body text) is slightly spaced out, which has the overall effect of lightening the page by creating more white space.

```
/*** text-properties.css ***/
h1 {
 word-spacing: -.1em;
}
h2 {
 word-spacing: 3px;
}
p {
 word-spacing: .075em;
}
.pageheader h2 {
 word-spacing: -.3em;
}
.pageheader h2 .cite {
 word-spacing: 0;
}
```

![](bbox=[0.07, 0.51, 0.45, 0.69])

> Code 6.3 applied to Code 6.1: The space between the words has been changed for effect in the titles and slightly increased to lighten the copy.

# Adjusting space between words

Just as tracking and word spacing adjustments can both help and hinder legibility, adding a little space between words on the screen using the word-spacing property (Table 6.2) can make your text easier to read. But too much space interrupts the path of the reader’s eye across the screen and interferes with reading.

# To define word spacing:

+   1. Add the word-spacing property to your declaration list. Type word-spacing in the CSS declaration list, followed by a colon (:) (Code 6.3).

+   2. Specify the amount of space between words.

Set the value for word-spacing, using one of the following:

+   > A positive or negative length value, representing the amount of space between words (-.1em, for example). For more information, see “Values and Units Used in This Book” in the Introduction.

+   > normal, which overrides inherited values.

> TIP Like letter spacing, use word spacing very sparingly. Generally, the natural word spacing has been optimized for readability. Changing that spacing often does more harm than good.