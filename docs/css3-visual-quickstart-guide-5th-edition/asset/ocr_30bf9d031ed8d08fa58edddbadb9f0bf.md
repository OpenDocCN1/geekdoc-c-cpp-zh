# # Changing the Mouse Pointer Appearance

# TABLE 9.1 Cursor Values

Normally, the browser determines the appearance of the mouse pointer according to the current content under it. If the pointer is over text, for example, the pointer becomes a text selector. Or, if the browser is working and the visitor can't do anything, the pointer becomes a timer, indicating that the visitor needs to wait.

| Value | Compatibility |
| --- | --- |
| <cursor type name> | IE4, FF1, S1, S0, C1, CSS2 |
| <URL> | IE6, FF1.5, S3, C3, CSS2 |
| auto | IE4, F1, S1, S0, C1, CSS2 |
| none | IE4, FF1, S1, S0, C1, CSS2 |

Sometimes, it's useful to override the browser's behavior and set the appearance of the mouse pointer yourself, using the cursor property (Table 9.1). This can be applied to any element on the screen, not just links. Also, you do not have to associate it with the dynamic hover state for it to work; just apply it directly to the CSS rule.

Code 9.2 ui-generated-content properties—I've set up different pointer types that depend on the type of object or link over which the pointer is hovering

```
*** CSS V05 | Chapter 9 |
- ui-generated-content.properties css ***

.toc { margin: auto; width: 90%;
 text-align: center; font-size: .5em; }

a {
 cursor: help;
}
```

# To set the mouse pointer's appearance:

+   1. Add the cursor property to your CSS declarations. Type cursor in the CSS declaration block, followed by a colon (1) Code 9.2).

+   2. Specify the mouse pointer. Type one of the mouse pointer names listed in Table 9.2 to specify the pointer's appearance.

CURSOR:

crosshair;

Alternatively, type one of these values for cursor:

+   - auto to have the browser choose which pointer to use.

+   - none to hide the pointer alterog.

![](bbox=[0.547, 0.558, 0.977, 0.765])

> Code 9.2 applied to code 9.1: the pointer turns into the Cheshire Cat's head when over the book title.