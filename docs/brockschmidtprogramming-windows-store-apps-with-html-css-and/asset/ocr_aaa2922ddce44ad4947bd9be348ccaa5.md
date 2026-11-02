To correct this, we'll need to dynamically determine the largest image dimension we can use within the current display area and then scale the image to that size while preserving the aspect ratio and keeping the image centered in the display. For centering purposes, the easiest solution I've found is to this is to create a surrounding div with a CSS grid wherein we can use row and column centering. So in default html:

```
~~~html
<div id="photo" class="graphic">
  <img id="photoImg" src="#" alt="Tap to capture image from camera" role="img" />
</div>
~~~
```

and in default.css:

```
~~~css
#photo {
  display: -ms-grid;
  -ms-grid-columns: 1fr;
  -ms-grid-rows: 1fr;
}

#photoImg {
  -ms-grid-column-align: center;
  -ms-grid-row-align: center;
}
~~~
```

The graphic style class on the div always scales to 100% width and height of its grid cell, so the one row and column within it will also occupy that full space. By adding the centering alignment to the photoImg child element, we know that the image will be centered regardless of its size.

To scale the image in this grid cell, then, we either set the image element's width style to 100% if its aspect ratio is greater than that of the display area, or set its height style to 100% if the opposite is true. For example, on a 1366x768 display, the size of the display area in landscape view is 583x528 for an aspect ratio of 1.1, and let's say we get an 800x600 image back from camera capture with an aspect ratio of 1.33. In this case the image is scaled to 100% of the display area width, making the displayed image 583x437 with blank areas on the top and bottom. Conversely, in 50% view the display area on the same screen is 612x249 with a ratio of 2.46, so we scale the 800x600 image to 100% height, which comes out to 332x249 with blank areas on the left and right.

The size of the display area is readily obtained through the clientWidth and clientHeight properties of the surrounding div we added to the HTML. The actual size of the captured image is then readily available through its StorageFile object's properties.getImagePropertiesAsync method. Putting all this together, here's a function that sets the appropriate style on the img element given its parent div and the captured file:

```
~~~javascript
function scaleImageToFit(imgElement, parentDiv, file) {
    file.properties.getImagePropertiesAsync().done(function (props) {
        var scaleToWidth =
            (props.width / props.height > parentDiv.clientWidth / parentDiv.clientHeight);
        imgElement.style.width = scaleToWidth ? "100%" : "";
        imgElement.style.height = scaleToWidth ? "" : "100%";
    }, function (e) {
        console.log("getImageProperties error: " + e.message);
    });
}
~~~
```