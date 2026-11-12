# ★Querying the Media

In Chapter 3 you learned how to specify style sheets for a particular media type, allowing you to set styles depending on whether the HTML is output to a screen, print, TV, or a handheld or other device (Table 4.7). CSS3 adds an important new capability that allows you to set styles based on common interface properties such as width, height, aspect ratio, and number of available colors.

Media queries and the @media rule can be used to tailor your page, not just to a general device type but to the specific device your site visitor is using. This includes sizing for print, for mobile devices, or to best fit the size of the open browser window.

# Media queries

If you want to know the current size of the browser window, why not just ask the browser? JavaScript gives you the ability to do this, but it’s a cumbersome way to get some basic facts about the Webbed environment your design is trying to fit into.

Media queries provide you with several common media properties that you can test (4) and then deliver the style sheet that best suits the environment.

Although media queries have many properties (Table 4.8), they come in five basic flavors:

+   Aspect-ratio looks for the relative dimensions of the device expressed as a ratio: 16:9, for example.

+   Width and height looks for the dimensions of the display area. These can also be expressed as maximum and minimum values.

| Value | Intended for |
|---|---|
| screen | Computer displays |
| tty | Teletypes, computer terminals, and older portable devices |
| tv | Television displays |
| projection | Projectors |
| handheld | Portable phones and PDAs |
| print | Paper |
| braille | Braille tactile readers |
| speech | Speech synthesizers |
| all | All devices |

```
media="
screen
and (min-width: 740px)
and (max-width: 980px)"
```

The general syntax for media queries.