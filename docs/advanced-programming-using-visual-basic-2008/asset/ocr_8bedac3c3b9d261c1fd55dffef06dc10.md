property to a different language, you can enter the Text property of each control in the current language. A separate resource file is created for each language that you select (Figure 13.20).

![](bbox=[0.091, 0.211, 0.429, 0.578])

# Figure 13.20

> A resource file is created for each language. The specific file holds the text strings for the language.

The CultureInfo class contains an associated language, sublanguage, calendar, and access to cultural conventions for number formatting, date formatting, and comparisons of strings. Table 13.4 shows a partial list of the choices; see the Help files for CultureInfo Class for a complete listing of all of the culture/code values. To use the CultureInfo class in a program, you must import the System.Globalization namespace.

# A Partial Listing of the Values for the CultureInfo Class

| CultureInfo value | Language—Country/region |
|---|---|
| af | Afrikaans |
| af-ZA | Afrikaans—South Africa |
| ca | Catalan |
| zh-HK | Chinese—Hong Kong SAR |
| zh-CHS | Chinese (Simplified) |
| en-CA | English—Canada |
| en-GB | English—United Kingdom |
| en-US | English—United States |
| fr-FR | French—France |
| es-ES | Spanish—Spain |
| es-MX | Spanish—Mexico |
| de-DE | German—Germany |

# Table 13.4