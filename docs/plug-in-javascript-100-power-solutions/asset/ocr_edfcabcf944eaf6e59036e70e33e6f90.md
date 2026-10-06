# 246 Plug-In JavaScript: 100 Power Solutions

```
HideToggle(a)
var iid = setInterval(RollCheck, INTERVAL)

function RollCheck() {
  if (MOUSE_X < x || MOUSE_X > x + w ||
      MOUSE_Y < y || MOUSE_Y > y + h) {
    HideToggle(a)
    clearInterval(iid)
  }
}
```

# 68 Breadcrumbs()

This-plugin provides an automatic trail of “breadcrumbs” leading from any location between a website's home page to the current page. With it, users can backtrack to the current page and the home page with a single click. Figure 8-11 shows the plug-in being used on a page in a local file system on a Windows PC.

# About the Plug-in

This plug-in returns the HTML to create a breadcrumb trail from the current web page to the home page. It requires the following argument:

+   - spacer A string of characters to place between each breadcrumb

# Variables, Arrays, and Functions

| parts | Local array containing the URL of the current page split into parts |
| crumbs | Local array that builds the breadcrumbs |
| title | Local variable containing the title of the current web page, if any |
| url | Local variable containing the URL of the website |
| display | Local variable containing the main HTML to return |
| j | Local variable for iterating through different arrays |
| push() | Function to push a value onto an array |
| InsVars() | Plug-in to insert values into a array |

# How It Works

This plug-in fetches the path to the current page from self.location.href and splits it by the ? character (if there is one) to extract the main URL from any query string. The string before the ? is split again at every / character, with the result being placed in the array paths.

After that, the crumbs array is created, which will be built up to contain the path. It is assigned an initial value of parts[0] (which will be http: or ftp: and so on), followed by the string '///', like this: