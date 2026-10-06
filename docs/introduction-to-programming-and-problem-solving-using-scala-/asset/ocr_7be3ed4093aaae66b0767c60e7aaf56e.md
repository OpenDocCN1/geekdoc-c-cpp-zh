```
else if {
    camera = new ParallelCamera
}

val useTexture = new CheckBox("Texture Sphere")
useTexture.layoutY = 300
useTexture.setOnAction = (e:ActionEvent) => {
    if (useTexture.selected) {
        sphereMaterial.diffuseMap = marsImage
        sphereMaterial.diffuseColor = Color.White
    } else {
        sphereMaterial.diffuseMap = null
        sphereMaterial.diffuseColor = Color.Red
    }
}

val ambientPicker = new ColorPicker(ambient.color.value)
ambient.color <== ambientPicker.value
ambientPicker.layoutY = 330

val pointPicker = new ColorPicker(point.color.value)
point.color <== pointPicker.value
pointPicker.layoutY = 360

content = List(sphere, cylinder, box, ambient, point, usePerspective,
    useTexture, ambientPicker, pointPicker)
```

A possible output of this program can be seen in figure 12.18.

# 12.12 Putting It Together

Given the breadth of this chapter, and the fact most of the sections had their own examples highlighting usage of the elements in a program, we are not going to attempt to write a single application that pulls everything together. It is not really clear that such a thing would ever make sense.