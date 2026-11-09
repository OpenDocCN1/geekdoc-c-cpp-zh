
![](img/5a907eb39993e80f28c82efc2e4632b3_198_0.png)

> **“After the button is pressed, find the customer’s current location”:**  
> The HTML syntax for your button code is:

```html
<button onclick="getLocation()">McDuck's Check-in</button>
```

The syntax for calling a JavaScript function by pressing a button is available here: w3schools.com/jsref/event_onclick.asp.

> **“Find the fixed location of a McDuck’s store”:** I picked a McDonald’s store in New York City near Madison Square Park whose latitude is 40.7410344 and longitude is −73.9880763. The latitude and longitude for your restaurant, of course, will likely differ.

> **“Calculate the distance between the customer’s current location and the McDuck’s restaurant, and name this distance Customer Distance”:** The following is the actual code for the Haversine formula, used to calculate the distance between two location coordinates, found on Stackoverflow at stackoverflow.com/questions/27928/how-do-i-calculate-distance-between-two-latitude-longitude-points. I modified this code slightly so that it returned miles instead of kilometers:

```javascript
function getDistanceFromLatLonInKm(lat1,lon1,lat2,lon2) {
    var R = 6371; // Radius of the earth in km
    var dLat = deg2rad(lat2-lat1); // deg2rad below
    var dLon = deg2rad(lon2-lon1);
    var a =
        Math.sin(dLat/2) * Math.sin(dLat/2) +
        Math.cos(deg2rad(lat1)) * Math.cos(deg2rad(lat2)) *
        Math.sin(dLon/2) * Math.sin(dLon/2)
        ;
    var c = 2 * Math.atan2(Math.sqrt(a), Math.sqrt(1-a));
    var d = R * c * 0.621371; // Distance in miles
    return d;
}

function deg2rad(deg) {
    return deg * (Math.PI/180);
}
```

An explanation of how this formula works is outside the scope of this book, but make sure you understand the formula’s inputs (latitude and longitude) and the output (distance between two points in miles).

![](img/5a907eb39993e80f28c82efc2e4632b3_198_1.png)

> **“Convert five to ten minutes of customer travel into a distance called Threshold Distance”:** In New York City, people usually walk, so traveling for five to ten minutes would take you 0.5 miles, which is my Threshold Distance.

> **“If the Customer Distance is less than the Threshold Distance, then display an offer to the customer”.** The syntax for the `if-else` statement with the two text `alert()` methods is:

```javascript
if (distance < 0.5) {
    alert('You get a free burger');
}
else {
    alert('Thanks for checking in!');
}
```

The syntax for a JavaScript if-else statement is available at www.w3schools.com/js/js_if_else.asp.

![](img/5a907eb39993e80f28c82efc2e4632b3_199_0.png)

## Coding and Debugging Your First Web Application

### In This Chapter

- Reviewing code to see pre-existing functionality
- Writing code by following steps to create your app
- Debugging your code by looking for common syntax errors

> Talk is cheap. Show me the code.
>
> —Linus Torvalds

It may not feel like it, but you’ve already done the majority of work toward creating your first web application. You painfully broke down your app into steps, and researched each step to determine functionality and design. As Linus Torvalds, creator of the Linux operating system, said, “Talk is cheap.” So let’s start actually coding.

### Getting Ready to Code

Before you start coding, do a few housekeeping items. First, ensure that you are doing all of the following:

- **Using the Chrome browser:** Download and install the latest version of Chrome, as it offers the most support for the latest HTML standards, and is available for download at `www.google.com/chrome/browser`.
- **Working on a desktop or laptop computer:** Although it is possible to code on a mobile device, it can be more difficult and all layouts may not appear properly.

![](img/5a907eb39993e80f28c82efc2e4632b3_202_0.png)

Figure 12-1: The Codepen.io development environment.

### Pre-written code

The Codepen.io development environment includes some pre-written HTML, CSS, and JavaScript code for the McDuck’s app. The pre-written code includes code you have seen in previous chapters, and new code that is explained below:

- **HTML:** The HTML code for the McDuck’s app is below, and includes:
  - Two sections: an opening and closing `<head>` tag, and an opening and closing `<body>` tag.
  - Inside the `<body>` tags are `<h1>` tags to create a heading and `<div>` tags.
  - Additional `<div>` tags to display messages created in the JavaScript file. The `<div>` tag is a container that can hold content of any type. The first `<div>` tag is used to display your current longitude and latitude. The second `<div>` tag can be used to display additional content to the user.
  - Instructions to insert the HTML button and `onclick` attribute code, which you researched in previous chapters.

Here’s the HTML code:

```html
<!DOCTYPE html>
<html>
<head>
    <title>McDuck's App</title>
</head>
<body>
    <h1>McDuck's Local Offers</h1>
    <!---1. Create a HTML button that when clicked calls the JavaScript
                 getLocation() function -->

    <!---Two containers, called divs, used to show messages to user -->

    <div id="geodisplay"></div>
    <div id="effect"></div>

</body>
</html>
```

↗ **CSS:** The CSS code for the McDuck’s app is below, and includes:

- Selectors for the body, heading, and paragraph tags.
- Properties and values that set the text alignment, background color, font family, font color, and font size.

Once your app is functioning, style the app by adding a McDuck’s color scheme and background image logo.

Here’s the CSS:

```css
body {
    text-align: center;
    background: white;
}

h1, h2, h3, p {
    font-family: Sans-Serif;
    color: black;
}

p {
    font-size: 1em;
}
```

↗ **JavaScript:** The JavaScript code for the McDuck’s app is below. This pre-written code is a little complex, because it calculates the current location of the user using the HTML Geolocation API. In this section I review the code at a high level so you can understand how it works and where it came from.

The Geolocation API is the product of billions of dollars of research and is available to you for free. The most recent browsers support geolocation, though some older browsers do not. At a basic level, code is written to ask whether the browser supports the Geolocation API, and, if yes, to return the current location of the user. When called, the Geolocation API balances a number of data inputs to determine the user’s current location. These data inputs include GPS, wireless network connection strength, cell tower and signal strength, and IP address.

With this in mind, let’s look at the JavaScript code. The JavaScript code includes two functions, as follows:

- *The `getLocation()` function:* This function determines whether the browser supports geolocation. It does this by using an `if` statement and `navigator.geolocation`, which is recognized by the browser as part of the Geolocation API and which returns a true value if geolocation is supported.

Here is the `getLocation()` function:

```
function getLocation() {
    if (navigator.geolocation){
        navigator.geolocation.getCurrentPosition(showLocation);
    }
}
```

- *The `showLocation()` function:* When the browser supports geolocation, the next step is to call the `showLocation` function, which calculates and displays the user’s location.

And here is the `showLocation()` function:

```
function showLocation(position){
// 2. Hardcode your store location on line 12 and 13, and update
//    comment to reflect your McDuck’s restaurant address
// Nick's at Perry & W 4th St (change to your restaurant location)

var mcduckslat=40.735383;
var mcduckslon=-74.002994;

// current location
var currentpositionlat=position.coords.latitude;
var currentpositionlon=position.coords.longitude;

// calculate the distance between your current location and McDuck's location
var distance=getDistanceFromLatLonInMiles(mcduckslat, mcduckslon,currentpositionlat,currentpositionlon);

// Displays the location using .innerHTML property and the lat & long
//                 coordinates for your current location
```
