```
~~~java
families.setValue("System");

EventHandler<ActionEvent> listener = event ->
{
    int size = (int) group.getSelectedToggle().getUserData();
    Font font = Font.font(
        families.getValue(),
        bold.isSelected() ? FontWeight.BOLD : FontWeight.NORMAL,
        italic.isSelected() ? FontPosture.ITALIC : FontPosture.REGULAR,
        size);
    sampleText.setFont(font);
};
small.setOnAction(listener);
medium.setOnAction(listener);
large.setOnAction(listener);
extraLarge.setOnAction(listener);
bold.setOnAction(listener);
italic.setOnAction(listener);
families.setOnAction(listener);

VBox root = new VBox(0.8 * rem,
    hbox(sampleText),
    hbox(bold, italic),
    hbox(small, medium, large, extraLarge),
    hbox(families));

stage.setScene(new Scene(root));
stage.setTitle("ChoiceTest");
stage.show();

}
~~~
```

| javafx.scene.control.CheckBox |
|---|
| • `CheckBox(String text)`<br>  constructs a checkbox labeled with the given text.<br>• `boolean isSelected()`<br>• `void setSelected(boolean value)`<br>  gets or sets the selected state of this checkbox. |

| javafx.scene.control.RadioButton |
|---|
| • `RadioButton(String text)`<br>  constructs a radio button labeled with the given text. |