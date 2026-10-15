Table 11.2: Showing the Properties of the Typography Class

| Property | Description |
|---|---|
| ContextualLigatures | Gets or sets a value that determines whether contextual ligatures are enabled. Contextual ligatures enhance readability of text by providing better joining behavior between the characters of the text. |
| ContextualSwashes | Gets or sets a value that specifies the index of a contextual swash. |
| DiscretionaryLigatures | Gets or sets a value that determines whether the combination of two or more words is enabled. |
| EastAsianExpertForms | Gets or sets a value that determines whether the standard Japanese font forms have been replaced with the preferred typographic forms. |
| EastAsianLanguage | Gets or sets a FontEastAsianLanguage enumerated value that indicates the version of glyphs to be used for a specific writing system or language. |
| EastAsianWidths | Gets or sets a FontEastAsianWidths enumerated value that indicates the proportional width to be used for Latin characters in an East Asian Font. |
| Fraction | Gets or sets a FontFraction enumerated value that indicates if fraction can be displayed or not. |
| HistoricalForms | Gets or sets a value that determines whether styles of text which are not commonly used are enabled. These types of text are called historical forms. |
| HistoricalLigatures | Gets or sets a value that determines whether historical ligatures are enabled. |
| Kerning | Gets or sets a value that indicates whether kerning is enabled. Kerning is the process of adjusting white spaces in between the characters in a proportion. |
| MathematicalGreek | Gets or sets a value that indicates whether standard typographic font forms of Greek glyphs have been replaced with corresponding font forms commonly used in mathematical notation. |
| NumeralAlignment | Gets or sets a FontNumeralAlignment enumerated value that indicates the alignment of text width while using numerals. |
| NumeralStyle | Gets or sets a FontNumeralStyle enumerated value that determines the style of glyph used to render numeric alternate font forms. |
| SlashedZero | Gets or sets a value that indicates whether a nominal zero font form is replaced with a slashed zero. A slashed zero is the simple zero with a slash before it. |
| StandardLigatures | Gets or sets a value that indicates whether standard ligatures are enabled. |
| StandardSwashes | Gets or sets a value that specifies the index of a standard swashes form. |
| StylisticAlternates | Gets or sets a value that specifies the index of stylistic alternate form. Stylistic alternates are the standard set of glyphs that are used to display text in different styles. |
| Variants | Gets or sets a FontVariants enumerated value that indicates a variation of the standard typographic form to be used in the text. |

**NOTE**
You cannot directly create an instance of the Typography class in the Extensible Application Markup Language (XAML) code. The instance of this class is created in the code-behind file.

# Transform Classes

In WPF, with the help of typography, you can apply transformations to the text. For example, you can rotate, scale, skew, or transform the text. You can use the Transform classes to transform the text. These classes also simplify the use of various drawings in the text. The most commonly used Transform classes are as follows: