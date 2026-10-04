case search, which means it lists items that have each word in the property begin with the letters you're searching for. In this case, bc matches items such as background-clip, background-color, and the same applies to all other CSS properties. For example, td would give you text-decoration, bbw gives you border-bottom-width, and so on. This makes it extremely easy to write CSS with only a few keystrokes.

Note some items in the list have an icon with a pair of scissors instead of the standard property icon. The scissors indicate a code snippet that you can expand by pressing Tab twice. Doing so inserts browser-specific CSS into the file that is used for CSS properties that are not yet implemented by all browsers.

Continue this exercise by selecting background-color from the list. You can double-click the value, press Enter or Tab, and VS completes the property for you. Next, type a color, a colon, and then the hash symbol (#) followed by cocococo (which represents the color silver). Close the line with a semicolon. Your final code could look like this:

```
header {
  background-color: #C0C0C0;
}
```

+   6. Complete the code block for the header element by adding width and height properties like this:
{
  background-color: #C0C0C0;
  width: 844px;
  height: 86px;
}

+   7. Complete the CSS file by creating the following rules. Make good use of Visual Studio's IntelliSense and title search feature to minimize the number of keystrokes to write this code.
*
n  font-family: Arial;
}
h1 {
  font-size: 20px;
}
#PageWrapper {
  width: 844px;
  margin: auto;
}
nav {
  width: 844px;
}