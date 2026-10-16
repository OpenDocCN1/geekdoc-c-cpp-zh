```
<input data-val="true"
    data-val-length="The field Text must be a string with a maximum length of 50."
    data-val-length-max="50"
    data-val-required="The Text field is required."
    id="FileName_Text" name="Text"
    type="text"
    value="Schweinsbraten mit Kn&ouml;del und Sauerkraut" />
```

# Working with Editor Extensions

Instead of using at least one helper method for every property, helper methods from the class `EditorExtensions` offer an editor for all the properties of a type.

Using the same `Menu` model as before, with the method `Html.EditorFor(m => m)` the complete user interface (UI) for editing the menu is built. The result from this method invocation is shown in Figure 41.9.

![](bbox=[0.105, 0.355, 0.895, 0.77])

# Figure 41.9

Instead of using `Html.EditorFor(m => m)`, you can use `Html.EditorForModel`. The method `EditorForModel` makes use of the model of the view without the need to specify it explicitly. `EditorFor` has more flexibility in using other data sources (for example, properties offered by the model), and `EditorForModel` needs fewer parameters to add.