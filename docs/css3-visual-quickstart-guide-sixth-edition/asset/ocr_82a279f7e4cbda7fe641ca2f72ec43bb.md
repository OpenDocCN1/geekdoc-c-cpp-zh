# # Adjusting space between lines of text (leading)

Anyone who has typed a term paper knows that they are usually double-spaced to make reading easier and allow space for comments. The leading between lines also can be increased for a dramatic effect by creating negative space between the text. The line-height property (Table 6.3) adds space between the text baselines (the bottoms of most letters).

# ## To define leading:

+   1. Add the line-height property to your rule. Type line-height in the CSS declaration list, followed by a colon (:) (Code 6.4).

line-height:

+   2. Specify the space between lines of text.

1.5;

Type a value for line-height, using one of the following options:

+   * A number to be multiplied by the font size to get the spacing value (2.0 for double-spacing, for example). Although a value of 2 works, it will not validate properly, so always include the decimal.

+   * A length value, such as 24px. The space for each line of text is set to this size regardless of the designated font size. So if the font size is set to 12px and the line height is set to 24px, the text will be double-spaced. See “Values and Units Used in This Book” in the Introduction.

+   * A percentage, which sets the line height proportionate to the font size used for the text.

+   * normal, which overrides inherited spacing values.

| Value | | | | | |
|---|---|---|---|---|---|
| normal | ● | ● | ● | ● | ● |
| <number> | ● | ● | ● | ● | ● |
| <length> | ● | ● | ● | ● | ● |
| <percentage> | ● | ● | ● | ● | ● |

Code 6.4 Added to text-properties.css—The default line-height has been set in the body to be 1.5, but paragraph copy has been set to 2em. That will double-space the text.

```
```css
/*** text-properties.css ***/
body { line-height: 1.5; }
p { line-height: 2em; }
h2 + p:first-letter {
line-height: 24px; }
```
```