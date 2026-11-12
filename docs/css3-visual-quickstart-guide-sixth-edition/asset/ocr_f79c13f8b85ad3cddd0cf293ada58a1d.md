4. Sets the style if the string is in a hyphenated list of values assigned to the property. To set styles based on an attribute's value being the first in a list separated by hyphens, type the selector you want to style (HTML, class, or ID), a left bracket ([), the name of the attribute you want to check for, a bar (|), an equals sign (=), the value you are testing for in quotes ('...'), and a right bracket (]).

```
a[title|="resume"]
```

This will assign the styles you declare only if the tag has this attribute assigned to it with a value that contains the string at the beginning of a hyphen-separated list. Generally, this is used for styling languages as an alternative to using the language pseudo-class.

5. ★Set styles if a string is the value's prefix. To set styles based on the value at the beginning of an attribute, type the selector you want to style (HTML, class, or ID), a left bracket ([), the name of the attribute you want to check for, a caret (^), an equals sign (=), the value you are testing for in quotes ('...'), and a right bracket (]).

```
a[href^="http://"]
```

This will assign the styles you declare only if the value string occurs exactly as it is in the quotes at the beginning of the attribute value.