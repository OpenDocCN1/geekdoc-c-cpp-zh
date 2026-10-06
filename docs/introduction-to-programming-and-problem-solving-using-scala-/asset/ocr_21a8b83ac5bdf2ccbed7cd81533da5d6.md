# 11.5.4 Pickers

There are types of values that the program needs to work with frequently, that require more complex interfaces for them to be easier to use. These include things like colors and dates. ScalFX includes ColorPicker and DatePicker controls for just this purpose. Each of appears normal like something like ComboBox, but when the user clicks on, they are presented with controls that allow them to select from various colors or a calendar that allows them to pick dates. Here is some code that uses these two controls.

Listing 11.9: PickerControls.scala

```
import scalfx.Includes..
import scalfx.scene.Scene
import scalfx.application.JFXApp
import scalfx.scene.control.Label
import scalfx.scene.control.ColorPicker
import scalfx.scene.control.DatePicker
import scalfx.scene.paint.Color
import scalfx.event.ActionEvent
import java.time.LocalDate
```

```
val app = new JFXApp {
  stage = new JFXApp.PrimaryStage {
    title = "Picker Controls"
    scene = new Scene(250,130) {
      // Label
      val label = new Label("Shows date once selected.")
      label.layoutX = 20
      label.layoutY = 20

      // ColorPicker
      val colorPicker = new ColorPicker(Color.White)
      colorPicker.layoutX = 20
      colorPicker.layoutY = 50

      // DatePicker
      val datePicker = new DatePicker(LocalDate.now)
      datepicker.layoutX = 20
      datepicker.layoutY = 80

      content = List(label, colorPicker, datePicker)

      colorPicker.onAction = (e:ActionEvent) => {
        fill = colorPicker.value.value
      }

      datepicker.onAction = (e:ActionEvent) => {
        label.text = "Date is : " + datePicker.value.value
      }
    }
  }
}
app.main(args)
```