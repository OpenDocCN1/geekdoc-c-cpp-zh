# Using the @media rule

Media queries allow you specify styles in the media property of <link> and <style> tags, but the @media rule allows you to embed media queries directly into a style sheet.

# Using @media to specify styles:

+   1. Create your style sheets. Create an external style sheet or embed a style sheet in the body of your document (Code 4.19).

+   2. Use the @media rule to specify styles with media queries. In the head of your HTML document, type @ and media. Then specify the media type (Table 4.7) and any media queries (Table 4.8) for the styles.

```
@media screen and ~ (max-device-width: 480px) (...)
```

For example, you might specify that these styles are for screens with a width up to 480px wide. Finish with curly brackets. Add any media-specific styles between the curly brackets.

+   3. Add other styles as necessary.

```
body {...}
```

You can add more @media rules or other nonmedia-specific rules. However, all CSS rules that are not in @rules (@media, @font-face, @import, and so on) must come after the @rules.

> TIP Remember that @media rules can go in external or embedded style sheets.

![](bbox=[0.53, 0.065, 0.94, 0.225])

F The general syntax of the @media rule.

![](bbox=[0.53, 0.28, 0.94, 0.475])

G Code 4.19 on a computer screen.

![](bbox=[0.53, 0.52, 0.85, 0.865])

H Code 4.19 on a mobile device screen. The styles and background have been modified based on the device width.