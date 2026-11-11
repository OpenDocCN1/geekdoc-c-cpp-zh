Instead, it waits for a short interval to see if the activity has already been completed or is likely to complete in less time than it would take for the dialog box to appear.

Use the `setMillisToDecideToPopup` method to set the number of milliseconds to wait between the construction of the dialog object and the decision whether to show the pop-up at all. The default value is 500 milliseconds. The `setMillisToPopup` is your estimation of the time the dialog box needs to pop up. The Swing designers set this value to a default of 2 seconds. Clearly they were mindful of the fact that Swing dialogs don't always come up as snappily as we all would like. You should probably not touch this value.

# **Listing 10.27** progressMonitor/ProgressMonitorFrame.java

```
```java
1 package progressMonitor;
2
3 import java.awt.*;
4
5 import javax.swing.*;
6
7 /**
8  * A frame that contains a button to launch a simulated activity and a text area for the activity
9  * output.
10  */
11 class ProgressMonitorFrame extends JFrame
12 {
13    public static final int TEXT_ROWS = 10;
14    public static final int TEXT_COLUMNS = 40;
15
16    private Timer cancelMonitor;
17    private JButton startButton;
18    private ProgressMonitor progressDialog;
19    private JTextArea textArea;
20    private SimulatedActivity activity;
21
22    public ProgressMonitorFrame()
23    {
24       // this text area holds the activity output
25       textArea = new JTextArea(TEXT_ROWS, TEXT_COLUMNS);
26
27       // set up a button panel
28       JPanel panel = new JPanel();
29       startButton = new JButton("Start");
30       panel.add(startButton);
31
32       add(new JScrollPane(textArea), BorderLayout.CENTER);
33       add(panel, BorderLayout.SOUTH);
34
35       // set up the button action
```
```