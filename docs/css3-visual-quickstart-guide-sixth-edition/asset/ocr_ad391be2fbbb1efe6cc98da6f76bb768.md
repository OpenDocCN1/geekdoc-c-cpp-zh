# Styling siblings

Siblings are elements that have the same parent. You can style a sibling that is immediately adjacent to another ⑥ or occurs anywhere after that sibling ⑦.

# To define adjacent sibling selectors:

+   1. Set up a list of adjacent sibling selectors. Type the selector for the first element (HTML, class, or ID), a plus sign (+), and then the selector (HTML, class, or ID) for the adjacent element to which you want the style applied (Code 4.4).

```
strong + em {...}
```

+   2. Styles will be used only if the pattern is matched.

```
<strong>...</strong><em>...</em>
```

The styles will be applied to any sibling that occurs immediately after the preceding selector with no other selectors in the way. Placing any element between them (even a break tag) will disrupt the pattern. The following pattern will not work:

```
<strong>...</strong>...<q>...</q>... <em>...</em>
```

![](bbox=[0.53, 0.07, 0.91, 0.23])

![](bbox=[0.53, 0.26, 0.91, 0.42])