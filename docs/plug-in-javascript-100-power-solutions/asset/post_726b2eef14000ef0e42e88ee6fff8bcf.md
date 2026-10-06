
## Chapter 8: Menus and Navigation 245

Here's an example that uses two single objects to create a rollover effect for a classified ad:

```html
<div id='r1'>
<img id='p1' src='palace.png' align='left'>
For sale: 600 room, 300 year old central London house, located
close to all the amenities, right in the heart of Westminster City.
</div>
```

```html
<div id='r2'>
<img id='p2' src='plan.png' align='right'>
829.18 sq ft: Historical setting, famous residents, exquisitely
detailed throughout. Phone 555 1234 for more details.
</div>
```

```javascript
<script>
window.onload = function () {
  rolls = Array('r1', 'r2');
  S(rolls, 'border', 'solid 1px');
  Resize(rolls, 320, 100)
  S('p1').paddingRight = P(10)
  S('p2').paddingLeft = P(10)
  Rollover('r1', 'r2')
}
</script>
```

The HTML section creates two divs and places some text and an image in each. Then the <script> section creates the rolls, which adds a border to each and resizes them to 320 by 100 pixels.

A couple of the S plug-ins set up padding around the images so that the text doesn't align right against them, and then the Rollover() plug-in is called to combine the two objects into a single rollover.

### Plug-in

```javascript
function Rollover(rol, ro2) {
  if (rol instanceof Array) {
    for (var j = 0; j < rol.length; ++j)
      Rollover(rol[j], ro2[j])
    return
  }

var a = Array(rol, ro2)
var w = W(rol) + 1
var h = H(rol) + 1
var x = X(rol)
var y = Y(rol)

Hide(ro2)
Locate(a, REL, 0, 0)
O(rol).onmouseover = DoRoll

function DoRoll() {

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

### Breadcrumbs()

This-plugin provides an automatic trail of “breadcrumbs” leading from any location between a website's home page to the current page. With it, users can backtrack to the current page and the home page with a single click. Figure 8-11 shows the plug-in being used on a page in a local file system on a Windows PC.

### About the Plug-in

This plug-in returns the HTML to create a breadcrumb trail from the current web page to the home page. It requires the following argument:

- spacer: A string of characters to place between each breadcrumb

### Variables, Arrays, and Functions

| parts | description |
| :--- | :--- |
| parts | Local array containing the URL of the current page split into parts |
| crumbs | Local array that builds the breadcrumbs |
| title | Local variable containing the title of the current web page, if any |
| url | Local variable containing the URL of the website |
| display | Local variable containing the main HTML to return |
| j | Local variable for iterating through different arrays |
| push() | Function to push a value onto an array |
| InsVars() | Plug-in to insert values into an array |

### How It Works

This plug-in fetches the path to the current page from self.location.href and splits it by the ? character (if there is one) to extract the main URL from any query string. The string before the ? is split again at every / character, with the result being placed in the array paths.

After that, the crumbs array is created, which will be built up to contain the path. It is assigned an initial value of parts[0] (which will be http: or ftp: and so on), followed by the string '///', like this:

FIGURE 8-11
Breadcrumbs provide a quick and easy website navigation aid.

![](img/95e4c43b430487125c342550cc090977_264_0.png)

```javascript
var parts = self.location.href.split('?')[0].split('/')
var crumbs = Array(parts[0]) + '/'
```

A next for (j) loop iterates all but the first two elements of the array to reassemble the URL into the crumbs using the push() function, as follows:

```javascript
for (var j = 2; j < parts.length; ++j)
  if (parts[j] == '') crumbs[0] += '/'
  else crumbs.push(parts[j])
```

The next three lines of code extract the title of the page (if any), the main URL of the website, and the:

```javascript
var title = document.title ? document.title : ''
var url = crumbs[0] + '/'
display = InsVars("<a href='#1'>Home</a>")
```

The InsVars() function inserts values into an array, and display is the string. If no spacer is supplied, spacer is the default:

```javascript
if (spacer == undefined) spacer = '/'
```

The InsVars() function inserts values into an array, and display is the string. If no spacer is supplied, spacer is the default:

```javascript
if (spacer == undefined) spacer = '/'
```

The InsVars() function inserts values into an array, and display is the string. If no spacer is supplied, spacer is the default:

```javascript
if (spacer == undefined) spacer = '/'
```

The InsVars() function inserts values into an array, and display is the string. If no spacer is supplied, spacer is the default:

```javascript
if (spacer == undefined) spacer = '/'
```

The InsVars() function inserts values into an array, and display is the string. If no spacer is supplied, spacer is the default:

```javascript
if (spacer == undefined) spacer = '/'
```

The InsVars() function inserts values into an array, and display is the string. If no spacer is supplied, spacer is the default:

```javascript
if (spacer == undefined) spacer = '/'
```

The InsVars() function inserts values into an array, and display is the string. If no spacer is supplied, spacer is the default:

```javascript
if (spacer == undefined) spacer = '/'
```

The InsVars() function inserts values into an array, and display is the string. If no spacer is supplied, spacer is the default:

```javascript
if (spacer == undefined) spacer = '/'
```

### Plug-In JavaScript: 100 Power Solutions

### BrowserWindow()

Didn't you have pop-ups before came with blockers? In my view, there is nothing wrong with the concept of pop-ups, it was just too easy for websites to inundate you with, and once everyone started using them it turned into a nightmare.

However, when I set up an Internet radio station in the 990s, I used pop-ups to good effect by implementing them as an audio player so that people could listen to the radio while they continued to surf in the main browser window. Perhaps due to the novelty, of the website's visitors kept these pop-ups open for long periods as they listened to.

Even though they have a bad name nowadays, pop-ups do plenty of uses, such as providing alerts and instant messages, for example. This-plugin provides a versatile in-browser pop-up that's more user friendly opening a new browser pop-up which will generally get blocked. It also gives the user full control, as it can be moved around the browser and is easily dismissible.

With this-plugin, you can ask for their login details, display private messages from another user in a forum, provide a selection of options, and so on. Or, as in Figure 8-12, you can pop up a window to provide further details when a user clicks a link. The great thing about it is the user has full control. You can keep the window raised and moved to reveal any content it was covering, or you can simply close it.

### Plug-In JavaScript: 100 Power Solutions

### BrowserWindow()

This-plugin creates an in-browser pop-up window that can be moved by the user and also popped back again. It requires the following:

* id An object or object ID identifying the main container—this may not be an array
* headerid An object or object ID identifying the draggable header
* closeid An object or object ID identifying the close button
* **x&&y** The top left coordinates of the pop-up

```html
<div id='r1'>
<img id='p1' src='palace.png' align='left'>
For sale: 600 room, 300 year old central London house, located
close to all the amenities, right in the heart of Westminster City.
</div>
```

```html
<div id='r2'>
<img id='p2' src='plan.png' align='right'>
829.18 sq ft: Historical setting, famous residents, exquisitely
detailed throughout. Phone 555 1234 for more details.
</div>
```

```javascript
<script>
window.onload = function () {
  rolls = Array('r1', 'r2');
  S(rolls, 'border', 'solid 1px');
  Resize(rolls, 320, 100)
  S('p1').paddingRight = P(10)
  S('p2').paddingLeft = P(10)
  Rollover('r1', 'r2')
}
</script>
```

The HTML section creates two divs and places some text and an image in each. Then the <script> section creates the rolls, which adds a border to each and resizes them to 320 by 100 pixels.

A couple of the S plug-ins set up padding around the images so that the text doesn't align right against them, and then the Rollover() plug-in is called to combine the two objects into a single rollover.

### Plug-in

```javascript
function Rollover(rol, ro2) {
  if (rol instanceof Array) {
    for (var j = 0; j < rol.length; ++j)
      Rollover(rol[j], ro2[j])
    return
  }

var a = Array(rol, ro2)
var w = W(rol) + 1
var h = H(rol) + 1
var x = X(rol)
var y = Y(rol)

Hide(ro2)
Locate(a, REL, 0, 0)
O(rol).onmouseover = DoRoll

function DoRoll() {

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

### Breadcrumbs()

This-plugin provides an automatic trail of “breadcrumbs” leading from any location between a website's home page to the current page. With it, users can backtrack to the current page and the home page with a single click. Figure 8-11 shows the plug-in being used on a page in a local file system on a Windows PC.

### About the Plug-in

This plug-in returns the HTML to create a breadcrumb trail from the current web page to the home page. It requires the following argument:

- spacer: A string of characters to place between each breadcrumb

### Variables, Arrays, and Functions

| parts | description |
| :--- | :--- |
| parts | Local array containing the URL of the current page split into parts |
| crumbs | Local array that builds the breadcrumbs |
| title | Local variable containing the title of the current web page, if any |
| url | Local variable containing the URL of the website |
| display | Local variable containing the main HTML to return |
| j | Local variable for iterating through different arrays |
| push() | Function to push a value onto an array |
| InsVars() | Plug-in to insert values into an array |

### How It Works

This plug-in fetches the path to the current page from self.location.href and splits it by the ? character (if there is one) to extract the main URL from any query string. The string before the ? is split again at every / character, with the result being placed in the array paths.

After that, the crumbs array is created, which will be built up to contain the path. It is assigned an initial value of parts[0] (which will be http: or ftp: and so on), followed by the string '///', like this:

FIGURE 8-11
Breadcrumbs provide a quick and easy website navigation aid.

![](img/95e4c43b430487125c342550cc090977_264_0.png)

```javascript
var parts = self.location.href.split('?')[0].split('/')
var crumbs = Array(parts[0]) + '/'
```

A next for (j) loop iterates all but the first two elements of the array to reassemble the URL into the crumbs using the push() function, as follows:

```javascript
for (var j = 2; j < parts.length; ++j)
  if (parts[j] == '') crumbs[0] += '/'
  else crumbs.push(parts[j])
```

The next three lines of code extract the title of the page (if any), the main URL of the website, and the:

```javascript
var title = document.title ? document.title : ''
var url = crumbs[0] + '/'
display = InsVars("<a href='#1'>Home</a>")
```

The InsVars() function inserts values into an array, and display is the string. If no spacer is supplied, spacer is the default:

```javascript
if (spacer == undefined) spacer = '/'
```

### Plug-In JavaScript: 100 Power Solutions

### BrowserWindow()

Didn't you have pop-ups before came with blockers? In my view, there is nothing wrong with the concept of pop-ups, it was just too easy for websites to inundate you with, and once everyone started using them it turned into a nightmare.

However, when I set up an Internet radio station in the 990s, I used pop-ups to good effect by implementing them as an audio player so that people could listen to the radio while they continued to surf in the main browser window. Perhaps due to the novelty, of the website's visitors kept these pop-ups open for long periods as they listened to.

Even though they have a bad name nowadays, pop-ups do plenty of uses, such as providing alerts and instant messages, for example. This-plugin provides a versatile in-browser pop-up that's more user friendly opening a new browser pop-up which will generally get blocked. It also gives the user full control, as it can be moved around the browser and is easily dismissible.

With this-plugin, you can ask for their login details, display private messages from another user in a forum, provide a selection of options, and so on. Or, as in Figure 8-12, you can pop up a window to provide further details when a user clicks a link. The great thing about it is the user has full control. You can keep the window raised and moved to reveal any content it was covering, or you can simply close it.

### BrowserWindow()

This-plugin creates an in-browser pop-up window that can be moved by the user and also popped back again. It requires the following:

* id An object or object ID identifying the main container—this may not be an array
* headerid An object or object ID identifying the draggable header
* closeid An object or object ID identifying the close button
* **x&&y** The top left coordinates of the pop-up
