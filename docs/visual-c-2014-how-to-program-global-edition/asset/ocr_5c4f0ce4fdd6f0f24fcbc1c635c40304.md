# 15.15 Wrap-Up

white background to make it stand out in the Form. Figure 15.50 shows the output of Clock, which contains our ClockUserControl. There are no event handlers in Clock, so we show only the code for ClockUserControl.

# Sharing Custom Controls with Other Developers

Visual Studio allows you to share custom controls with other developers. To create a User-Control that can be exported to other solutions, do the following:

+   1. Create a new Class Library project.

+   2. Delete Class1.cs, initially provided with the app.

+   3. Right click the project in the Solution Explorer and select Add > User Control.... In the dialog that appears, name the user-control and click Add.

+   4. Inside the project, add controls and functionality to the UserControl (Fig. 15.51).

![](bbox=[0.437, 0.388, 0.562, 0.473])

Fig. 15.51 | Custom-control creation.

+   5. Build the project. Visual Studio creates a .dll file for the UserControl in the output directory (bin/Debug or bin/Release). The file is not executable; class libraries are used to define classes that are used in other executable apps. You can give the .dll file to other developers and they can follow Steps 6 and 7.

+   6. Create a new Windows app.

+   7. In the new Windows app, right click the Toolbox and select Choose Items.... In the Choose Items dialog that appears, click Browse.... for the .dll file from the class library created in Steps 1–5. The item will then appear in the .NET Framework Components tab of the Choose Items dialog. If it's not already checked, check this item. Click OK to add it to the Toolbox. This control can now be added to the Form as if it were any control.

# 15.15 Wrap-Up

Many of today's commercial apps provide GUIs that are easy to use and manipulate. Because of this demand for user-friendly GUIs, the ability to design sophisticated GUIs is an essential programming skill. Visual Studio's IDE makes GUI development quick and easy. In Chapters 14 and 15, we presented Basic Forms development techniques, which provide users access to an app functionality. You learned the DateTime and MonthCalendar controls, which allow users to input date and time values. We demonstrated Linklabels, which are used to link the user to an app or a web page. You used several controls that provide lists of data to the user—ListBoxes, CheckedListBoxes and ListViews. We used