# Font or Font Family?

Keep in mind the difference between a font and a font family. A font family is a series of fonts with similar appearance—such as Times—where a font refers to a specific version—such as Times normal, Times bold, Times italic, and so on.

+   3. Define a list of alternative fonts, called understand fonts, separated by commas. You can include as many as you want. These fonts will be used (in the order specified) if the previous font in the list is not available on the visitor's computer. See "Why Include Understudy Fonts" in this chapter for more details.

Arial1,

# Why Include Understudy Fonts and Generic Font Families?

+   4. Define the generic font family. After the last understudy font, type the name of the generic font family for the particular style of font you're using. Table 5.1 lists generic values for families. Although including this value is optional, doing so is a good idea.

When you provide a list of fonts, the browser tries to use the first font on list. If it isn't available, the browser continues through the list until it finds a font that is installed on the visitor's computer. If no match is found, the browser displays the text in the visitor's default font. The advantage of using a generic font is that the browser tries to display the text in the same style of font, even if the specific fonts on the list are not available.

Sans-serif;

+   5. Add typeface overrides. After a font is set for the body of the page, it will be used in all text throughout the Web page, with the exception of text in forms. You will need to add font-family declaration to your CSS only if you want to change the font for a particular element. This is due to the fact that properties cascade to their child elements, described in chapter 4.

As a last resort, you can include the generic font so that a browser can make an intelligent decision on the closest matching.

The exception to the cascade rule are form elements such as input, text, area, button, etc., which require their fonts to be set in the form element to cascade down.

The advantage of using understudy and generic font families is, even if a desired font is not available, you can still control which font is used in its place, or at least, get a match.

```
font-family: Georgia, Times, 'Times New Roman', Serif;
```

+   TIP Try to choose fonts with a similar size. Different fonts will have relative sizes even if set to the same font size.

+   TIP If you are using bold,italic, and/or bold-italic/oblique versions of the font, be sure that the font family supports all of these typefaces. If not, the text will not display properly or worse, the browser will try to synthesize these versions. Either way, the results will not look professional.

Some typefaces are easy to read on a screen; others look better when printed. Always consider the destination when choosing your fonts.