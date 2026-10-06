# Introduction to Programming and Problem-Solving Using Scala

```
button.onClick = (e:ActionEvent) => {
  label.text = "Button clicked"
}

cb1.onClick = (e:ActionEvent) => {
  label.text = "Check Box 1 is " + cb1.selected.value
}
cb2.onClick = (e:ActionEvent) => {
  label.text = "Check Box 2 is " + cb2.selected.value
}

rb1.onClick = (e:ActionEvent) => {
  label.text = "Radio Button 1 is " + rb1.selected.value
}
rb2.onClick = (e:ActionEvent) => {
  label.text = "Radio Button 2 is " + rb2.selected.value
}
rb3.onClick = (e:ActionEvent) => {
  label.text = "Radio Button 3 is " + rb3.selected.value
}
rb1.selected.onChange = (println("Radio button 1 is " + rb1.selected.value))

tb1.onClick = (e:ActionEvent) => {
  label.text = "Toggle Button 1 is " + tb1.selected.value
}
tb2.onClick = (e:ActionEvent) => {
  label.text = "Toggle Button 2 is " + tb2.selected.value
}
tb3.onClick = (e:ActionEvent) => {
  label.text = "Toggle Button 3 is " + tb3.selected.value
}
tb1.selected.onChange = (println("Toggle button 1 is " + tb1.selected.value))

app.main(args)
```

All of the button-like controls allow you to define onClick, which is called when the user clicks on button. For the RadioButton and the ToggleButton, the state of selection can also change when the user selects one of the other elements. This does not fire the action handler, but you can set up code to be called when that type of change occurs by setting the onChange value of the selected member, as shown in the code. To do this was only added for the first RadioButton and ToggleButton.

# 11.5.3 Selection Controls

There are controls that allow the user to select different items from a designated selection. The ComboBox and ListView appeared in earlier examples. There is also a ChoiceBox, which is very similar to the ComboBox in functionality and appearance, but can allow multiple selections. Here is code that adds these three components to a Scene and handles the user making selections on them.