# # Creating Multicolumn Layouts with Float

The most common way to lay out a page is by establishing a grid, which is generally made up of two or more columns This allows the designer to present multiple sources of information and functionality in the same horizontal plane, making better use of the screen and reducing the need to scroll.

Although not explicitly intended to perform this duty, the float property (discussed in Chapter 10) is now the standard method for creating a grid structure of columns in most modern Web designs. This is done by taking block level elements that would normally stack vertically and horizontally and “floating” them next to each other

The basic wireframe for your page, showing the three columns within the surrounding element.

| header |
| section |
| nav | article | aside |
| footer |

# ### Set up a multicolumn layout using CSS:

+   1. Create an external CSS file called layout.css (Code 14.2).

```
layout.css
```

This file contains the CSS needed to create your grid and is linked to your HTML in Code 14.1.

+   2. Add rules to define the width of your content. This generally Involves defining a width for the site's header and footer, as well as the section into which you will add the articles. The width depends on your design needs, but 980 pixels is a typical width for many Web pages:

| article |
| aside | nav | aside |
| No Floating | Floating |

```
header.site, section,
footer.site {..}
```

When floating is applied, the columns horizontally next to each other.

continues on page 349