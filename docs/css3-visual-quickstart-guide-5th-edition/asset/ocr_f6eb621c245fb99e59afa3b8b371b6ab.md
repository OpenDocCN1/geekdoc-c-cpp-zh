# Setting Text Case

When you're dealing with dynamically generated output, such as from a database, you can never be quite sure whether the text will appear in uppercase, lowercase, or a combination of the two. With the **text-transform** property (Table 6.4), you can control the case of the text no matter how it enters.

TABLE 6.4 Text-Transform Values
| Value | Compatibility |
| --- | --- |
| capitalize | IE4, FF1, S1, C1, O3, CSS1 |
| uppercase | IE4, FF1, S1, C1, O3, CSS1 |
| lowercase | IE4, FF1, S1, C1, O3, CSS1 |
| none | IE4, FF1, S1, C1, O3, CSS1 |

To define the text case:

+   1. Add the text-transform property to your CSS. Type `text-transform` in the CSS declaration list, followed by a colon (**Code 6.4**).

+   2. Specify the text case.
   uppercase:
   Type one of the following **text-transform** values to specify how you want the text to be treated:
   **capitalize** sets the first letter of each word to uppercase.
   **uppercase** forces all letters to uppercase.
   **lowercase** forces all letters to lowercase.
   **none** overrides inherited text-case values and leaves the text unaltered.

**Code 6.5** text-properties.css—The **text-transform** property lets you take control of the case of the text. The author is forced to capitalize as the class `.asis`.

```
*** CSS3 V5 | Chapter 6 | text-properties.
/ css ***/

body {
  line-height: 1.5;
}

h1 {
  letter-spacing: -0em;
  word-spacing: -1em;
  line-height: .9em;
}

h2 {
  letter-spacing: 2px;
  word-spacing: 3px;
}

h2 strong {
  letter-spacing: 0;
}

p {
  word-spacing: .07em;
  line-height: 24px;
}

header + p:first-letter {
  letter-spacing: -0em;
  line-height: 24px;
}

byline {
  word-spacing: -.3em;
}

byline .author {
  word-spacing: 0;
  text-transform: uppercase;
}

.asis {
  text-transform: uppercase;
}
```