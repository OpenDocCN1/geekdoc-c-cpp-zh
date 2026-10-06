
# Introduction to Programming and Problem-Solving Using Scala

![](img/06d4e84f27a8884ea40ba6182ec7c778_324_0.png)

**FIGURE 11.12:** This figure shows the window that results from running Others.scala after adjusting the various elements.

```scala
sliderLabel.layoutY = 100

content = List(progress, scroll, scrollLabel, separator, slider, toolBar,
sliderLabel)

advButton.setOnAction = (e:ActionEvent) => {
progress.value = progress.value + 0.05 min 1.0 max 0.0
}

decButton.setOnAction = (e:ActionEvent) => {
progress.value = progress.value - 0.05 min 1.0 max 0.0
}

scroll.value.onChange = {
scrollLabel.text = "Scroll bar = " + scroll.value.value
}

slider.value.onChange = {
sliderLabel.text = "Slider = " + slider.value.value
}
```

The top of the window has the ToolBar with four buttons. There is a Separator between the first two buttons and the second buttons. The main area is divided in half by another Separator.

On the left side of the main area is a ProgressBar and a ScrollBar. The first two buttons in the ToolBar control the ProgressBar. By default, the ProgressBar has a negative value which causes it to be animated. For example, at the time of this writing shows a blue bar that moves back and forth across the field. The buttons can be used to increase or decrease the value. When these are clicked, you can show the indicator move. Figure 11.12
The ScrollBar is set to go from 0 to 100, and when the value changes, the Label below the ScrollBar changes to tell what the value is. By default the ScrollBar is horizontal. You can change it to a vertical orientation if you want.

The right side of the main area has the Slider, which also has a label below it, and that label is updated when the value of the Slider is changed.

## 11.6 Observables, Properties, and Bindings

A number of examples above have used things with names that included the words "Observable" or "Property". For example, both the ChoiceBox and the TableView used ObservableBuffer to hold the data that was placed into them. The columns for the TableView explicitly made objects with the types StringProperty and ObjectProperty. Though it was not explicit in the code, the text and focused members of the TextField are of type StringProperty and ReadOnlyProperty, respectively. It turns out that properties are all over the place in the code that we have written. The onChange typically followed a value, which was a Property. In addition to the ability to set onChange, these properties have capabilities that we have not explored. The most important of these is the ability to do things.

In the ScalFX library, an observable is, as the name implies, something that we observe in the code. What this means is that you can set it up so that other parts of the code are notified when the observed value changed. The reason for the ObservableBuffer in the TableView is that the table is observing the data. If you change the data, the table will be automatically updated. Note that this type of behavior does not happen by default. If you make a var and set a TextField to display value, an assignment does not affect the TextField. It happens that the text in the TextField is property, so there are other ways to get it to update that are automatic.

The way to make things updated automatically in the GUI is with bindings. You can bind a property to an observable of the proper type, and when the observable changes, the property will automatically be updated. You can also create bidirectional bindings between two properties, so that either one is changed, the other will be updated as well. To see how this works, we start off by modifying a few of the earlier examples so that they use bindings instead of the onChange method.

We begin with the code for the ColorPicker and DatePicker. In the original version, both set onChange to something. The following code shows how these can be replaced by appropriate bindings.

Listing 11.14: PickerBindings.scala

```scala
import scalafx.Includes._
import scalafx.scene.Scene
import scalafx.application.JFXApp
import scalafx.scene.control.Label
import scalafx.scene.control.ColorPicker
import scalafx.scene.control.DatePicker
import scalafx.scene.Color
import scalafx.beans.property.StringProperty
import java.time.LocalDate

val app = new JFXApp {
  stage = new JFXApp.PrimaryStage {
    title = "Picker Bindings"
    scene = new Scene(250,130) {
      // Label
```

```scala
val label = new Label("Shows date once selected.")
label.layoutX = 20
label.layoutY = 20
```

```scala
// ColorPicker
val colorPicker = new ColorPicker(Color.White)
colorPicker.layoutX = 20
colorPicker.layoutY = 50
```

```scala
// DatePicker
val datePicker = new DatePicker(LocalDate.now)
datePicker.layoutX = 20
datePicker.layoutY = 80
```

```scala
content = List(label, colorPicker, datePicker)
```

```scala
fill <= colorPicker.value

label.text <= StringProperty("Date is :") + datePicker.value.asString
```

```scala
}
}
```

app.main(args)
The only changes are at the end of the file, where the handling code had been. The ColorPicker object had been set so it would alter the fill property of the Scene when a change was made. Now that functionality is achieved with fill <= colorPicker.value. The <= operator creates a unidirectional binding. In this case, fill is bound to the value of colorPicker.value. When the value of the colorPicker is, the background color of the scene is automatically updated to reflect

Updating the text on the Label is a bit more complex, but only a bit. This is because we have a different type, and we also want to bind to a String that is more than the date itself. Again, the code that uses label.text <= StringProperty("Date is :") + datePicker.value.asString, the <= operator is used to actually create the binding. What we need to be a property, and more specifically a StringProperty, because the text is a StringProperty. Casting as String on datePicker.value gives us a StringProperty for that, but we also want to prepend "Date is :" concatenate them. This produces a new StringProperty that is itself.

### 11.6.1 Numeric Properties and Bindings

To illustrate what we can do with numeric bindings, we will use an example. This example has three Sliders that control the location and size of a rectangle. The first controls the horizontal location, the second controls the vertical location, and the third controls the size. There is also a ScrollBar that is bidirectionally bound to one of the Sliders to illustrate how one of elements change when you change the other. Lastly, there is a Label that is set to be centered on the window.

Listing 11.15: NumericBindings.scala

```scala
import scalafx.Includes._
import scalafx.scene.Scene
import scalafx.application.JFXApp
import scalafx.scene.control.Label
import scalafx.scene.control.Slider
import scalafx.scene.shape.Rectangle

val app = new JFXApp {
  stage = new JFXApp.PrimaryStage {
    title = "Numeric Bindings"
    scene = new Scene(600,250) {
      label = new Label("This stays centered.")

      val xSlider = new Slider(0,100,0)
      xSlider.layout = 10
      xSlider.layoutY = 10
      xSlider.prefWidth = 180

      val ySlider = new Slider(0,100,0)
      ySlider.layoutX = 210
      ySlider.layoutY = 10
      ySlider.prefWidth = 180

      val sizeSlider = new Slider(0,100,0)
      sizeSlider.layoutX = 410
      sizeSlider.layoutY = 10
      sizeSlider.prefWidth = 180

      val scroll = new ScrollBar
      scroll.layoutX = 220
      scroll.layoutY = 220
      scroll.min = 0
      scroll.max = 100
      scroll.prefWidth = 180

      val rectangle = Rectangle(10,10)
      rectangle.layoutX = 0
      rectangle.layoutY = 40

      content = List(label, xSlider, ySlider, sizeSlider, scroll, rectangle)
      label.layoutX <= (width.width)/2
      label.layoutY <= (height.height)/2
      rectangle.layoutX <= xSlider.value*6
      rectangle.layoutY <= ySlider.value+40
      rectangle.width <= (sizeSlider.value*2)+10
      rectangle.height <= (sizeSlider.value*2)+10
      scroll.value <= ySlider.value
    }
  }
}
app.main(args)
```
