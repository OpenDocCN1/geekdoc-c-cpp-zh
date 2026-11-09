
![](img/5a907eb39993e80f28c82efc2e4632b3_94_0.png)

Figure 6-4: The CSS rules that style the Huffington Post website.

![](img/5a907eb39993e80f28c82efc2e4632b3_94_1.png)

Figure 6-5: Changing the CSS changes the color of the headline.

## Common CSS Tasks and Selectors

Although CSS includes over 150 properties, and many values for each property, on modern websites a handful of CSS properties and values do the majority of the work. In the previous section, when you “hacked” the CSS on a live website, you changed the heading color — a common task in CSS. Other common tasks performed with CSS include:

- Changing font size, style, font family, and decoration
- Customizing links including color, background color, and link state
- Adding background images and formatting foreground images

## Font gymnastics: size, color, style, family, and decoration

CSS lets you control text in many HTML elements. The most common text-related CSS properties and values are shown in Table 6-1. I describe these properties and values more fully in the sections that follow.

**Table 6-1. Common CSS Properties and Values for Styling Text**

| Property name | Possible values | Description |
|---|---|---|
| `font-size` | `pixels (#px)`<br>`%`<br>`em (#em)` | Specifies the size of text measured either in pixels, as a percentage of the containing element’s font size, or with an em value which is calculated by desired pixel value divided by containing element font size in pixels. Example: `font-size: 16px;` |
| `color` | `name`<br>`hex code`<br>`rgb value` | Changes the color of the text specified using names (`color: blue;`), hexadecimal code (`color: #0000FF;`), or RGB (red, green, and blue) value (`color: rgb(0,0,255);`). |
| `font-style` | `normal`<br>`italic` | Sets font to appear in italics (or not). |
| `font-weight` | `normal`<br>`bold` | Sets font to appear as bold (or not). |
| `font-family` | `font name` | Sets the font typeface. Example: `font-family: "serif";` |
| `text-decoration` | `none`<br>`underline`<br>`line-through` | Sets font to have an underline or strikethrough (or not). |

```css
:root {
  --c-brand: #3081d0;
  --c-brand-light: #509acd;
  --c-border: #eee;
  --c-bg: #ffffff;
  --c-bg-dark: #1e1e1e;
  --c-scrollbar: #ddd;
  --c-text: #2c3e50;
  --c-text-light: #476582;
  --c-text-lighter: #8e9bab;
  --c-code-bg: #f7f7f7;
  --c-code-text: #2c3e50;
}

.dark {
  --c-brand: #3081d0;
  --c-brand-light: #509acd;
  --c-border: #444;
  --c-bg: #1e1e1e;
  --c-bg-dark: #1e1e1e;
  --c-scrollbar: #444;
  --c-text: #cfd3dc;
  --c-text-light: #9a9a9a;
  --c-text-lighter: #8e9bab;
  --c-code-bg: #282c34;
  --c-code-text: #cfd3dc;
}
```

- **Hex code:** Colors can be defined by component parts of red, green, and blue, and when using hexadecimal code over 16 million colors can be referenced. In the code example, I set the `h1` color equal to `#FF0000`. After the hashtag, the first two digits (`FF`) refers to the red in the color, the next two digits (`00`) refers to the green in the color, and the final two digits (`00`) refers to the blue in the color.
- **RGB value:** Just like hex codes, RGB values specify the red, green, and blue component parts for over 16 million colors. RGB values are the decimal equivalent to hexadecimal values.

![](img/5a907eb39993e80f28c82efc2e4632b3_97_0.png)

Don’t worry about trying to remember hex codes or RGB values. You can easily identify colors using an online color picker such as the one at www.w3schools.com/tags/ref_colorpicker.asp.

The following example shows all three types of color changes:

```css
p {
  color: red
}
h1 {
  color: #FF0000
}
li {
  color: rgb(255,0,0)
}
```

`li` is the element name for a list item in ordered or unordered lists.

![](img/5a907eb39993e80f28c82efc2e4632b3_97_1.png)

All three colors in the code example above reference the same shade of red. For the full list of colors that can be referenced by name see here: www.w3.org/TR/css3-color/#svg-color.

![](img/5a907eb39993e80f28c82efc2e4632b3_97_2.png)

### Setting the font-style and font-weight

The `font-style` property can set text to italics, and the `font-weight` property can set text to bold. For each of these properties, the default is normal, which doesn’t need to be specified. In the example below, the paragraph is styled so the font appears italicized and bold. Here’s an example of each:

```css
p {
  font-style: italic;
  font-weight: bold;
}
```

### Setting the font-family

The `font-family` property sets the typeface used for text. The property is set equal to one font, or to a list of fonts separated by commas. Your website visitors will have a variety of different fonts installed on their computers, but the `font-family` property displays your specified font only if that font is already installed on their system.

The `font-family` property can be set equal to two types of values:

- **Font name:** Specific font names such as Times New Roman, Arial, and Courier.
- **Generic font family:** Modern browsers usually define one installed font for each generic font family. These five generic font families include:
  - `serif` (Times New Roman, Palatino)
  - `sans-serif` (Helvetica, Verdana)
  - `monospace` (Courier, Andale Mono)
  - `cursive` (Comic Sans, Florence)
  - `fantasy` (Impact, Oldtown)

When using `font-family` it’s best to define two or three specific fonts followed by a generic font family as a fallback in case the fonts you specify aren’t installed, as in the following example:

```css
p {
    font-family: "Times New Roman", Helvetica, serif;
}
```

In this example, the paragraph’s font family is defined as Times New Roman. If Times New Roman isn’t installed on the user’s computer, the browser then uses Helvetica. If Helvetica is not installed, the browser will use any available font in the generic serif font family.

![](img/5a907eb39993e80f28c82efc2e4632b3_98_0.png)

When using a font name with multiple words (such as Times New Roman) enclose the font name in quotes.

### Setting the text-decoration

The `text-decoration` property sets any font underlining or strikethrough. By default, the property is equal to none, which does not have to be specified. In the following example, any text with an h1 heading is underlined whereas any text inside a paragraph tag is made strikethrough:

```css
h1 {
    text-decoration: underline;
}
p {
    text-decoration: line-through;
}
```

## Customizing links

In general, browsers display links as blue underlined text. Originally, this default behavior minimized the confusion between content on the page and an interactive link. Today, almost every website styles links in its own way. Some websites don’t underline links; others retain the underlining but style links in colors other than blue, and so on.

![](img/5a907eb39993e80f28c82efc2e4632b3_99_0.png)

The HTML anchor element (a) is used to create links. The text between the opening and closing anchor tag is the link description, and the URL set in the `href` attribute is the address the browser visits when the link is clicked.

The anchor tag has evolved over time and today has four states:

- **link:** A link that a user has not clicked or visited.
- **visited:** A link that a user has clicked or visited.
- **hover:** A link that the user hovers the mouse cursor over without clicking.
- **active:** A link the user has begun to click but hasn’t yet released the mouse button.

CSS can style each of these four states, most often by using the properties and values shown in Table 6-2.

**Table 6-2. Common CSS Properties and Values for Styling Links**

| Property name | Possible values | Description |
|---|---|---|
| `color` | `name`<br>`hex code`<br>`rgb value` | Link color specified using names (`color: blue;`), hexadecimal code (`color: #0000FF;`), or RGB value (`color: rgb(0,0,255);`). |
| `text-decoration` | `none`<br>`underline` | Sets link to have an underline (or not). |

The following example styles links in a way that’s similar to the way they’re styled in articles at Wikipedia, where links appear blue by default, underlined on mouse hover, and orange when active. As shown in Figure 6-6, the first link to Chief Technology Officer of the United States appears underlined as it would if my mouse was hovering over it. Also, the link to Google appears orange as it would if active and my mouse was clicking it.
