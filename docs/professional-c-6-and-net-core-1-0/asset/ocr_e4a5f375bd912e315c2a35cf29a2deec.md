Checking the result of the generated HTML code reveals that the `input` type Tag Helpers create a `type` attribute depending on the type of the property, and they also apply the `DataType` attribute. The property `Price` is of type double, which results in a number input type. Because the `Date` property has the `DataType` with a value of `DataType.Date` applied, the input type is a date. In addition to that you can see `data-val-length`, `data-val-length-max`, and `data-val-required` attributes that are created because of annotations:

```
<label for="Text">Menu</label>
<input type="text" data-val="true"
    data-val-length=
        "The field Menu must be a string with a maximum length of 50."
    data-val-length-max="50"
    data-val-required="The Menu field is required."
    id="FileName_Text" name="Text"
    value="Schweinsbraten mit Kn&ouml;del und Sauerkraut" />
<br/>
<label for="Price">Price</label>
<input type="number" data-val="true"
    data-val-required="The Price field is required."
    id="FileName_Price" name="Price" value="6.9" />
<br />
<label for="Date">Date</label>
<input type="date" data-val="true"
    data-val-required="The Date field is required."
    id="FileName_Date" name="Date" value="10/5/2016" />
```

Modern browsers have a special look for HTML 5 input controls such as date control. The input date control of Microsoft Edge is shown in Figure 41.10.

![](bbox=[0.1, 0.54, 0.9, 0.89])

Figure 41.10