This procedure also works for `StreamWriter` objects. The following two lines cause the Save As dialog box to open. The user can browse to the location where the file should be stored and either type a new filename or select a file to replace.

```
saveFileDialog1.ShowDialog( );
StreamWriter outFile = new StreamWriter(saveFileDialog1.FileName);
```

When these lines are executed, instead of the dialog box having the word Open in the title bar, as shown in Figure 13-14, the title bar will contain the words Save As.

# Programming Example: ICW WaterDepth File App

In Chapter 12, a graphical user interface solution was designed to enable users to enter areas along the ICW where boaters were advised to take warning because of shoaling or shallow water. The graphical user interface enabled users to enter a location name, state, mile marker number, and four separate days of water depth at low and high tide. When valid data was entered, a message was displayed showing the location and its associated data. However, after the data about a single location was processed and displayed, it was lost when the second and subsequent locations were entered. There was no mechanism available to store the data from one run to another run. For this programming example, the solution presented in Chapter 12 will be modified to allow the results to be captured and stored for future use.

# Analyze the Problem

You should review the problem specification in Figure 12-21 and make sure you understand the problem definition. Several values must be entered into the program. Instead of allowing a single set of location and associated depths to be entered, the application should allow multiple locations to be entered. A Windows application was developed as part of the solution for the programming example illustrated in Chapter 12. When a Windows application is run, it is put in a process loop and can handle multiple value sets. Minor modifications will be needed to ready the form for the second and subsequent set of input values.

# Data

Three classes were designed for the solution to the `WaterDepth` application in Chapter 12. You should review Table 12-4. It lists the data field members needed for the `ShoalArea` class. No new data members are needed for this class. No changes are needed for the `TestOfStateException` class. The `FrmWaterDepth` class created the user interface and displayed a message showing the problem area and its water depths. In this class, an object of the `StreamWriter` class will be created.