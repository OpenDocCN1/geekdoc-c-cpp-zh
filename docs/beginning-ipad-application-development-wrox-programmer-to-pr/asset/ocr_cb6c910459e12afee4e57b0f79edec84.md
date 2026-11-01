```
@property (nonatomic, retain) UIDatePicker *datePicker;
-(IBAction) doneEditing: (id) sender;
@end
```

![](bbox=[0.15, 0.27, 0.42, 0.5])

FIGURE 13-4

+   5. In Interface Builder:
+     - Control-click and drag the File's Owner item to the Textfield view and select textField.
+     - Control-click and drag the File's Owner item to the DatePicker view and select datePicker.
+   6. Right-click the TextField view and connect its Did End on Exit event to the File's Owner item (see Figure 13-5). Select doneEditing:.

![](bbox=[0.15, 0.64, 0.88, 0.88])

FIGURE 13-5