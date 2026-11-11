This dialog also shows an *expandable content* node that is revealed by clicking on “Show Details”—in our case, a text area containing an exception stack trace. Here is how you set such a node:

```
TextArea stackTrace = new TextArea();
alert.getDialogPane().setExpandableContent(stackTrace);
```

If you want to accept text input from the user, use a TextInputDialog, shown in Figure 13.27.

![](bbox=[0.424, 0.305, 0.663, 0.454])

**Figure 13.27** A text input dialog

The `showAndWait` method returns an `Optional<String>`, which is empty if the user clicked the Cancel button or dismissed the dialog. Here is one way of processing it:

```
TextInputDialog dialog = new TextInputDialog();
dialog.setHeaderText("What is your name?");
dialog.showAndWait().ifPresentOrElse(
    result -> { do something with result },
    () -> { deal with cancellation }
);
```

The ChoiceDialog class is similar. You provide a default choice and an array or list of choices. If the default is not null, it is selected when the dialog is shown (see Figure 13.28). The showAndWait method returns an Optional that contains the selected item, or is empty if the dialog was canceled.

```
ChoiceDialog<String> dialog = new ChoiceDialog<>("System", Font.getFamilies());
dialog.setHeaderText("Pick a font:");
Optional<String> choice = dialog.showAndWait();
```

The type parameter of the generic ChoiceDialog<T> class is the type of the choices. You can provide choices of any type, provided that their toString method yields meaningful strings for the combo box.