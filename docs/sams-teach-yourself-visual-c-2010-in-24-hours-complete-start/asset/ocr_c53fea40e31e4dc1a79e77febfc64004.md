# ## Subscribing to Events

To subscribe to events published by a user interface control in a Windows Forms application and a WPF application, follow these steps.

+   Open the Hour6 solution in Visual Studio.

+   Open Form1.cs in the EventsWinForms project by double-clicking the file.

+   In the design view for Form1, select the button and add an event handler for the Click event.

+   In the generated event handler method, add the following statement:

```
```
MessageBox.Show("You pressed the button.");
```
```

+   Run the application by pressing Ctrl+F5. When you click the button, you should see the following dialog appear, as shown in Figure 6.5.

![](bbox=[0.37, 0.46, 0.55, 0.56])

FIGURE 6.5  
Message box from the event handler

+   Open MainWindow.xaml in the EventsWpf project by double-clicking the file.

+   In the design view for MainWindow, select the button and add an event handler for the Click event. In the generated event handler method, add the same statement you added in step 4.

+   Run the application by right-clicking the project in the Solution Explorer window and selecting the Start new instance option from the Debug menu, as shown in Figure 6.6.

![](bbox=[0.23, 0.74, 0.68, 0.8])

FIGURE 6.6  
Solution Explorer context menu

+   When you click the button, you should see the following dialog appear, as shown in Figure 6.7.