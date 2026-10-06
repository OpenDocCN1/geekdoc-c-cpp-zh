The right side of the main area has the Slider, which also has a label below it, and that label is updated when the value of the Slider is changed.

# 11.6 Observables, Properties, and Bindings

A number of examples above have used things with names that included the words "Observable" or "Property". For example, both the ChoiceBox and the TableView used ObservableBuffer to hold the data that was placed into them. The columns for the TableView explicitly made objects with the types StringProperty and ObjectProperty. Though it was not explicit in the code, the text and focused members of the TextField are of type StringProperty and ReadOnlyProperty, respectively. It turns out that properties are all over the place in the code that we have written. The onChange typically followed a value, which was a Property. In addition to the ability to set onChange, these properties have capabilities that we have not explored. The most important of these is the ability to doings.

In the ScalFX library, an observable is, as the name implies, something that we observe in the code. What this means is that you can set it up so that other parts of the code are notified when the observed value changed. The reason for the ObservableBuffer in the TableView is that the table is observing the data. If you change the data, the table will be automatically updated. Note that this type of behavior does not happen by default. If you make a var and set a TextField to display value, an assignment does not affect the TextField. It happens that the text in the TextField is property, so there are other ways to get it to update that are automatic.

The way to make things updated automatically in the GUI is with bindings. You can bind a property to an observable of the proper type, and when the observable changes, the property will automatically be updated. You can also create bidirectional bindings between two properties, so that either one is changed, the other will be updated as well. To see how this works, we start off by modifying a few of the earlier examples so that they use bindings instead of the onChange method.

We begin with the code for the ColorPicker andth. In the original version, both set onChange to something. The following code shows how these can be replaced by appropriate bindings.

Listing 11.14: PickerBindings.scala

```
import scalafx.Includes._nimport scalafx.scene.Scene
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