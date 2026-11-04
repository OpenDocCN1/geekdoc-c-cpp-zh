```
label1.Font = new Font(label1.Font.Name, label1.Font.Size, label1.Font.Style |
    FontStyle.Italic);
}
```

The code given in Listing 5.11 changes the text font of label to italic when you select the Italic check box.

6 Press the F5 key to run the ControlApplication application and select the Red radio button and Bold check box, the output appears, as shown in Fig.C#5.38:

![](bbox=[0.35, 0.25, 0.6, 0.38])

Fig.C#5.38

In Fig.C#5.38, the text in label1 appears in red color and bold.

# Using the ListBox Control

ListBox control is a standard Windows control that is used to display text as a list. Text can be displayed as a sorted or an unsorted list. The ListBox control recognizes text as a collection of items. You can add text as an item into this collection to display it on a ListBox control. Similarly, you can remove an item from the list if you do not want to display it on the ListBox control. Each item in a ListBox control is recognized by its position in the list, which is known as its index.

Let's perform the following steps to use the ListBox control in a Windows Forms application:

+   1. Repeat steps 1 to 3 of the Changing the Title of a Form section of this chapter.
+   2. Enter ListAndComboBox in the Name text box and specify an appropriate location in the Location combo box.
+   3. Click the OK button. The ListAndComboBox application is created with the specified name and location.
+   4. Drag a ListBox control from Toolbox and drop it on the Form1 form (Fig.C#5.39).
+   5. Click the ellipsis button of the Items property in the Properties window of the ListBox control, as shown in Fig.C#5.39:

![](bbox=[0.35, 0.65, 0.7, 0.75])

Fig.C#5.39

The String Collection Editor dialog box opens (Fig.C#5.40).

+   6. Enter the required items in the String Collection Editor dialog box (Fig.C#5.40).
+   7. Click the OK button, as shown in Fig.C#5.40: