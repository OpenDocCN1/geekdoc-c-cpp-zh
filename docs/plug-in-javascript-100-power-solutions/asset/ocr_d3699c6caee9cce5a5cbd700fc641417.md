# Chapter 8: Menus and Navigation

FIGURE 8-11
Breadcrumbs provide a quick and easy website navigation aid.

![](bbox=[0.237, 0.107, 0.792, 0.263])

```
var parts = self.location.href.split('?')[0].split('/')
var crumbs = Array(parts[0]) + '/'
```

A next for (j) loop iterates all but the first two elements of the array to reassemble the URL into the crumbs using the push() function, as follows:

```
for (var j = 2; j < parts.length; ++j)
  if (parts[j] == '') crumbs[0] += '/'
  else crumbs.push(parts[j])
```

The next three lines of code extract the title of the page (if any), the main URL of the website, and the first breadcrumb, named 'Home', like this:

```
var title = document.title ? document.title : parts[1]
var url = crumbs[0] + crumbs[1]
var display = InsVars("<a href="#1">Home/</a>", url)
```

The InsVars() function inserts the url into the display string, replacing the #1. If no title is found, the filename of the current page is used instead. If no argument was supplied for the spacer to place between each breadcrumb, spacer is given the default value of a single space:

```
if (typeof spacer == UNDEF) spacer = '
```

After this, another for (j) loop extracts each element from the crumbs array and attaches it (prefixed with a character) to the display string with suitable HTML anchor tags, like this:

```
for (j = 2; j < crumbs.length; ++j)
  url += '/' + crumbs[j]
  display += spacer + InsVars("<a href="#1"></a>", url, crumbs[j])
```

Finally, the contents of display is returned, appended to another spacer string, followed by the page title:

```
return display + spacer + title
```