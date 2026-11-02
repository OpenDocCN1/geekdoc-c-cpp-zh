above for ImageProperties.

As for saving properties, the Simple Imaging sample delivers there as well, also in scenario 1. As the fields shown earlier in Figure 11-12 are editable, the sample provides an Apply button (panned off the top of the screen) that invokes the applyHandler function below to write them back to the file (js/scenario1.js):

```
```javascript
function applyHandler() {
  ImageProperties.title = id("propertiesTitle").value;

  // Keywords are stored as an array of strings. Split the textarea text by newlines.
  ImageProperties.keywords.clear();
  if (id("propertiesKeywords").value !== "") {
    var keywordsArray = id("propertiesKeywords").value.split("\n");

    keywordsArray.forEach(function (keyword) {
      ImageProperties.keywords.append(keyword);
    });
  }

  var properties = new Windows.Foundation.Collections.PropertySet();

  // When writing the rating, use the "System.Rating" property key.
  // ImageProperties.rating does not handle setting the value to 0 (no stars/unrated).
  properties.insert("System.Rating", Helpers.convertStarsToSystemRating(
    id("propertiesRatingControl").winControl.userRating
  ));

  // Code omitted: convert discrete latitude/longitude values from the UI into the
  // appropriate forms needed for the properties, and do some validation; the end result
  // is to store these in the properties list
  properties.insert("System.GPS.LatitudeRef", latitudeRef);
  properties.insert("System.GPS.LongitudeRef", longitudeRef);
  properties.insert("System.GPS.LatitudeNumerator", latNum);
  properties.insert("System.GPS.LongitudeNumerator", longNum);
  properties.insert("System.GPS.LatitudeDenominator", latDen);
  properties.insert("System.GPS.LongitudeDenominator", longDen);

  // Write the properties array to the file
  ImageProperties.savePropertiesAsync(properties).done(function () {
    // ...
  }, function (error) {
    // Some error handling as some properties may not be supported by all image formats.
  });
}
```
```

A few noteworthy features of this code include the following:

+   - It separates keywords in the UI control and separately appends each to the keywords property vector.
+   - It creates a new Windows.Foundation.Collections.PropertySet, which is the expected input to savePropertiesAsync. Remember from Chapter 6 that the PropertySet is the only