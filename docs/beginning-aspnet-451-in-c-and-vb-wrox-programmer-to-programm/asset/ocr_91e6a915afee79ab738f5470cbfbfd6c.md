# An Introduction to CSS | 75

Using named colors can increase the readability of your CSS code, but because you're limited to a relatively short list of named colors, you often need the hexadecimal notation to get the exact color you want. Later in this chapter you see how to use the built-in color picker to create the exact color you need.

Many other values are possible as well, including size units (px, em and so on), font families, images (which take the form of url(SomeImage.jpg)), and so-called enumerations like the border-style, which enables you to set a border style such as solid, dashed and double.

# Using Shorthand

Many of the CSS properties enable you to write a shorthand version as a more expanded version. Take, for example, the border property. In its shortest form, you can set the border property like this:

```
border: 1px solid Black;
```

This border property applies a border to all four sides of an HTML element. The border size is 1px, the style is solid (some of the other options include dashed, dotted, and double), and the border color is set to Black.

This is easy to quickly set all four borders of the HTML to the same values. However, if you want to control over the individual borders and their properties, you can use the expanded version:

```
border-top-width: 1px;
border-top-style: solid;
border-top-color: Black;
border-right-width: 1px;
border-right-style: solid;
border-right-color: Black;
border-bottom-width: 1px;
border-bottom-style: solid;
border-bottom-color: Black;
border-left-width: 1px;
border-left-style: solid;
border-left-color: Black;
```

This long version creates the exact same style as a solid border on all four sides with a thickness of 1px. In most cases, you should favor shorthand notation over its expanded counterpart, it is much easier to read and maintain. However, if you need absolute control over the border — for example, if you want a 2-pixel dashed border on the top and left, and a green, solid on the right and bottom sides of the HTML element — its good to know that you can set each border property of all directions individually. You can also mix these options.

```
border: 1px solid Black;
border-left-color: Blue;
```

Other CSS properties that support shorthand include font, background, list-style, margin, and padding. If you're unsure whether a property supports shorthand, the IntelliSense pop-up list appears by pressing Ctrl+Space when you're entering a property in a CSS file or a <style> block.