The term "cascading" in cascading style sheets refers to the order of precedence of style rules. More locally created styles override the rules of the more globally created styles. For example, you might apply an h1 style from the style sheet (global) that sets the font, color, size, and alignment. And if you also apply a style defined in the page for the color and size, the local (page-defined) color and size take precedence, but the font and alignment of the style-sheet style are still in effect. And if you also apply an inline style for the size, the inline (more local) style will override the size but keep the color of the page-defined style and the font and alignment of the style-sheet style.

# Types of Styles

In Visual Studio, you will use several new tools to define, apply, modify, and change the location of styles. The Apply Styles window and the Manage Styles window, both of which you will learn about in the next section, use the following icons in Table 7.1 to identify the various types of styles.

# Cascading Style Sheet (CSS) Style Types

| Icon | Style type | How referenced |
|---|---|---|
| • (Red dot) | ID-based style; defined in a .css file. Applies to a specific element by ID. | Style name preceded by a pound sign.
Example: #footer |
| • (Green dot) | Class-based style; defined in a .css file or the current page. Defines style properties that you want to apply to some, but not all, elements of a particular type, such as some (paragraph) elements. | Style name preceded by a period.
Example: .intro |
| • (Blue dot) | Element-based style; defined in the style block of a page. Applies to all elements that use a particular tag, such as <p> (for paragraph) or <td> (for table cell). | Style name only.
Example: p {margin-left: 25px; margin-right: 25px} |
| • (Yellow dot) | Inline style. Applies only to the specified item; will not be reused by another element. | In Design view, apply formatting such as font, size, and bold, from the Format menu or the formatting toolbar. In Source view, formatting appears using the style element of the opening tag.
Example: <p style="font-weight: bold; font-style: italic"> |
| * (Circled dot) | Indicates that the style is used on the current page. | A dot without a circle indicates that the style is defined but not used. |
| @ (At sign) | Indicates an imported external cascading style sheet. |  |

# New Style Tools

The Visual Studio 2008 IDE and Visual Web Developer have new windows that make it easy to define, apply, and manage styles. The new windows—CSS Properties, Manage Styles, and Apply Styles—appear by default in the same area as the toolbox and are available from the View menu. Also, a new Style Application toolbar appears in the default layout of the IDE. Figure 7.15 shows the new tools.

# The Style Application Toolbar

You can use the first drop-down list on the Style Application toolbar to select either Manual or Auto style application. The Auto selection disables the remaining