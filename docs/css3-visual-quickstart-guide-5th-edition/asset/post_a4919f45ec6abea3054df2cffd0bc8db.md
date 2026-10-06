
> TIP The pseudo-elements syntax in CSS3 has undergone a slight change from CSS2 syntax (which is rare). Pseudo-elements now have a double colon to distinguish them from pseudo-classes. Existing pseudo-elements can use single or double colons. New and future pseudo-elements should use double colons, but will work with a single colon.

- bullet-01.png and bullet-02.png will be used as flourishes around titles.
- Alice's Adventures in Wonderland

> TIP Since IE8 does not support double colon syntax for CSS2 pseudo-elements, it's a good idea to use colon syntax for now until all browsers have adopted the syntax.

The extinct Alice appeared, she was appealed by all to arrest the queen, and they proved their arguments, that they did so, but the queen was pleased to make execute exactly what she said.

The executioner's argument was, they couldn't cut off a head there was no way to it off them; he had better not to do such a thing, before, and he wasn't going to begin at 103 time of it.

> TIP Be careful when using before and after to add content to your page. This content will not appear to search engines or screen readers, so do not rely on it for anything vital.

The King's argument was, that anything that had a head could be behaved, and that you were to make sense.

The header now had a bit of flourish added before and after by the CSS. These images take up space as if they were in an image tag, but do not show up in the HTML code.

## Coming Soon!
Styling the Selection

Although not implemented in enough (or any) browsers to make it worth even thinking about yet, a great new pseudo-element is coming to CSS3, ::selection, which will style every element selected by the user.

## Defining Styles Based on Tag Attributes

Although by CSS, many HTML tags still have attributes that define how they behave. For example, the image tag, `<img>`, always includes the `src` attribute to define the source for the image file to be loaded.

Styles can also be assigned to an HTML element based on an attribute or an attribute value, allowing you to set styles if the attribute has been set, or is not a specific value, or contains a specific value (Table 4.6).

To set styles based on an element's attributes:

- 1. Set styles if the element has a specific property. To set styles based on the existence of an attribute, type the selector you want to style (HTML, class, or ID), a left bracket ([), the name of the attribute you want to check for, and a right bracket (]) (Code 4.13) `a[title] {...}`

![](img/9cd61ac1d4015ed5688d0c411434a660_119_0.png)

| Table 4.6 Attribute Selectors | Format | Name | Elements Are Styled If That Element | Compatibility |
| :--- | :--- | :--- | :--- |
| [attr] | Attribute | has specified attribute | IE7, FF1.5, O5, S2, CSS2 |
| [attr="value"] | Exact value | has specified attribute equal to exact value | IE7, FF1.5, O5, S2, CSS2 |
| [attr*=value] | Spaced List | has specified attribute equal to exact value within space-separated list | |
| [attr~value] | Hyphenated List | has specified attribute equal to exact value within hyphen-separated list | IE7, FF1.5, O5, S2, CSS2 |
| [attr^="value"] | Begins with | has specified attribute equal to exact value at beginning | CSS3 |
| [attr$="value"] | Ends With | has specified attribute equal to exact value at end | CSS3 |
| [attr*="value"] | Contains | has specified attribute equal to exact value anywhere | CSS3 |

## 4.13 HTML tags can have different attributes, and you can add styles to an element

This will assign the styles you declare only if the tag has this attribute assigned to it regardless of the value.

```html
<!-- HTML5 -->
<!DOCTYPE html>
<html lang="en">
<head>
  <meta http-equiv="Content-Type" content="text/html; charset=UTF-8">
  <title>Alice's Adventures in Wonderland/</title>
  <style type="text/css" css="display: block; color:rgb(0,0,0);
    font-size: 8em;
    a[title="home"] { color: rgb(51,0,0);
      font-size: 1em;
    a[title="email"] { color: rgb(102,0,0);
      font-size: 1.2em;
    a[title="resume"] { color: rgb(153,0,0);
      font-size: 1.4em;
    a[href="#info"] { color: rgb(240,0,0);
      font-size: 1.6em;
    a[href="#next"] { color: rgb(235,0,0);
      font-size: 1.8em;
    a[href="#speakinginstyles"] {
      font-size: 2em;}
  </style>
</head>
<body>
  <navigation>
    <h2>About the Author</h2>
    <a href="index.html" title="Portfolio">Portfolio</a>
    <a href="index.html" title="Home">Home</a>
    <a href="email.html" title="link-resume">RVsomvc</a>
    <a href="http://www.jsspeaking.com" title="blog">JasonSpeaking</a>
    <a href="http://www.fluidwebtype.info" title="book">Fluid Web Typography</a>
    <a href="http://www.speakinginstyles.com" title="book">Speaking In Styles</a>
  </navigation>
</body>
</html>
```

- 2. Set styles if a string exactly matches the property's value. To set styles based on an exact value, type the selector you want to style a left bracket ([), the name of the attribute you want to test (=), the value you are testing for in quotes ('...'). The value is case sensitive.

This will assign the styles you declare only if the tag has this attribute assigned to it with the exact assigned value.

continues on next page.

## About the Author

Portfolio
Home Page
Email
Résumé
JasonSpeaking
Fluid Web Typography
Speaking In Styles

> The results of Code 4.13 shows how styles are applied to elements based on their properties.

Selective Styling 97

- 3. Set styles if a string is in a space-separated list of values. To set styles based on an attribute's value that is within a list of space-separated values (for example, a particular word in a sentence), type the selector you want to style (HTML, class, or ID), a left bracket ([), the name of the attribute you want to check for, a tilde (~), an equals sign (=), the value you are testing for in quotes ('...'), and a right bracket (]).

```css
a[title~="email"] {..}
```

This will assign the styles you declare only if the tag has the attribute assigned to it with a value that contains the string as part of a space-separated list. Generally, this means that it is a word in a sentence. Partial words do not count. So in this example, testing for 'mail' would not work.

- 4. Sets the style if the string is in a hyphenated list. To set styles based on an attribute's value being the first in a hyphenated list, type the selector you want to style (HTML, class, or ID), a left bracket ([), the name of the attribute you want to check for, a bar (|), an equals sign (=), the value you are testing for in quotes ('...'), and a right bracket (]).

```css
a[title|="resume"]
```

This will assign the styles you declare only if the tag has the attribute assigned to it with a value that starts with the string.

- 5. NEW CSS3 ★ Set styles if a string is the value's prefix. To set styles based on the value beginning of an attribute, type the selector you want to style (HTML, class, or ID), a left bracket ([), the name of the attribute you want to check for, a caret (^), an equals sign (=), the value you are testing for in quotes ('...'), and a right bracket (]).

```css
a[href^="http://"]
```

This will assign the styles you declare only if the value string occurs exactly as it is in the quotes at the beginning of the attribute value.

- 6. NEW CSS3 ★ Set styles if a string is the property value's suffix. To set styles based on an attribute's value being the end of the string, type the selector you want to style (HTML, class, or ID), a left bracket ([), the name of the attribute you want to check for, a dollar sign ($), an equals sign (=), the value you are testing for in quotes ('...'), and a right bracket (]).

```css
a[href$=".info"]
```

This will assign the styles you declare only if the value occurs at the end of the attribute's value.

- 7 Set styles if a string is anywhere in the property value. To set styles based on an attribute's value being anywhere in the string, type the selector you want to style (HTML, class, or ID), a left bracket ([), the name of the attribute you want to check for, an asterisk (*), an equals sign (=), the value you are testing for in quotes ('...'), and a right bracket (]).

```css
a[href*="speakinginstyles"]
```

This will assign the styles you declare if the value occurs anywhere in the attribute's value.

Values are case sensitive. In other words, 'Alice' and 'alice' are two different values.
