The selector identifies which HTML element you want to style. In HTML, an element is surrounded by angle brackets, but in CSS the selector stands alone. The selector is followed by a space, an opening left curly bracket ({), property with a value, and then a closing right curly bracket (}). The line break after the opening curly bracket, and before the closing curly bracket is not required by CSS — in fact, you could put all your code on one line with no line breaks or spaces. Using line breaks is convention followed by developers to make CSS easier to modify and read.

![](bbox=[0.131, 0.259, 0.207, 0.332])

You can find curly brackets on most keyboards to the right of the P key.

The following code shows you an example of CSS modifying a specific HTML element. The CSS code appears first, followed by the HTML code that it modifies:

The CSS:

```
```css
h1 {
    font-family: cursive;
}
```
```

And now the HTML:

```
```html
<h1>
    Largest IPOs in US History
</h1>
<ul>
    <li>2014: Alibaba - $20B</li>
    <li>2008: Visa - $18B</li>
</ul>
```
```

The CSS selector targets and styles the HTML element with the same name (in this case, `<h1>` tags). For example, in Figure 6-2, the heading “Largest IPOs in US History,” featured using the opening and closing `<h1>` tags is styled using the h1 selector, and the `font-family` property with cursive value.

CSS uses a colon instead of the equals sign (=) to set values against properties.

![](bbox=[0.12, 0.646, 0.207, 0.724])

![](bbox=[0.131, 0.736, 0.207, 0.805])

The font in Figure 6-2 likely does not appear to be cursive, as defined in the code above, because cursive is the name of a generic font family, and not a specific font. Generic font families are described later in this chapter.

# My property has value

CSS syntax requires that a CSS property and its value appear within opening and closing curly brackets. After each property is a colon, and after each value is a semi-colon. This combination of property and value together is