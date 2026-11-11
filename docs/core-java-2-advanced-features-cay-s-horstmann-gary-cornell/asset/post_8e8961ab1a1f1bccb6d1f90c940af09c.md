
```java
editorPane.setText("Exception: " + e);
        }
    });
```

The event handler simply gets the URL and updates the editor pane. The setPage method can throw an IOException. In that case, we display an error message as plain text.

The program in Listing 10.25 shows all the features that you need to put together an HTML help system.

Under the hood, the JEditorPane is even more complex than the tree and table components. However, if you aren't writing a text editor or a renderer of a custom text format, that complexity is hidden from you.

### Listing 10.25 editorPane/EditorPaneFrame.java

```java
1 package editorPane;
2
3 import java.awt.*;
4 import java.awt.event.*;
5 import java.io.*;
6 import java.util.*;
7 import javax.swing.*;
8 import javax.swing.event.*;
9
10 /**
11  * This frame contains an editor pane, a text field and button to enter a URL and load a document,
12  * and a Back button to return to a previously loaded document.
13  */
14 public class EditorPaneFrame extends JFrame
15 {
16    private static final int DEFAULT_WIDTH = 600;
17    private static final int DEFAULT_HEIGHT = 400;
18
19    public EditorPaneFrame()
20    {
21       setSize(DEFAULT_WIDTH, DEFAULT_HEIGHT);
22
23       final Stack<String> urlStack = new Stack<>();
24       final JEditorPane editorPane = new JEditorPane();
25       final JTextField url = new JTextField(30);
26
27       // set up hyperlink listener
28
29       editorPane.setEditable(false);
30       editorPane.addHyperlinkListener(event ->
31       {
32          if (event.getEventType() == HyperlinkEvent.EventType.ACTIVATED)
33          {
34  try
35  {
36      // remember URL for back button
37      urlStack.push(event.getURL().toString());
38      // show URL in text field
39      url.setText(event.getURL().toString());
40      editorPane.setPage(event.getURL());
41  }
42  catch (IOException e)
43  {
44      editorPane.setText("Exception: " + e);
45  }
46 }
47 });
49 // set up checkbox for toggling edit mode
51 final JCheckBox editable = new JCheckBox();
52 editable.addActionListener(event ->
53     editorPane.setEditable(editable.isSelected()));
56 // set up load button for loading URL
58 ActionListener listener = event ->
59 {
60     try
61     {
62         // remember URL for back button
63         urlStack.push(url.getText());
64         editorPane.setPage(url.getText());
65     }
66     catch (IOException e)
67     {
68         editorPane.setText("Exception: " + e);
69     }
70 };
72 JButton loadButton = new JButton("Load");
73 loadButton.addActionListener(listener);
74 url.addActionListener(listener);
76 // set up back button and button action
78 JButton backButton = new JButton("Back");
79 backButton.addActionListener(event ->
80 {
81     if (urlStack.size() <= 1) return;
82     try
83        // get URL from back button
84        urlStack.pop();
85        // show URL in text field
86        String urlString = urlStack.peek();
87        url.setText(urlString);
88        editorPane.setPage(urlString);
89      }
90      catch (IOException e)
91      {
92        editorPane.setText("Exception: " + e);
93      }
94    });
96    add(new JScrollPane(editorPane), BorderLayout.CENTER);
98    // put all control components in a panel
100   JPanel panel = new JPanel();
101   panel.add(new JLabel("URL"));
102   panel.add(url);
103   panel.add(backButton);
104   panel.add(new JButton("Editable"));
105   panel.add(editable);
108   add(panel, BorderLayout.SOUTH);
109 }
110 }
```

| `javax.swing.JEditorPane` 1.2 |
| --- |
| • `void setPage(URL url)`<br>  loads the page from url into the editor pane.<br><br>• `void addHyperlinkListener(HyperlinkListener listener)`<br>  adds a hyperlink listener to this editor pane. |

| `javax.swing.event.HyperlinkListener` 1.2 |
| --- |
| • `void hyperlinkUpdate(HyperlinkEvent event)`<br>  is called whenever a hyperlink was selected. |

If you call

```java
progressBar.setStringPainted(true);
```

the progress bar computes the completion percentage and displays a string “n%”. If you want to show a different string, you can supply it with the setString method:

```java
if (progressBar.getValue() > 900)
    progressBar.setString("Almost Done");
```

The program in Listing 10.26 shows a progress bar that monitors a simulated time-consuming activity.

The SimulatedActivity class increments a value current ten times per second. When it reaches a target value, the activity finishes. We use the SwingWorker class to implement the activity and update the progress bar in the process method. The SwingWorker invokes the method from the event dispatch thread, so it is safe to update the progress bar. (See Volume I, Chapter 14 for more information about thread safety in Swing.)

Java SE 1.4 added support for an indeterminate progress bar that shows an animation indicating some kind of progress, without specifying the percentage of completion. That is the kind of progress bar that you see in your browser—it indicates that the browser is waiting for the server and has no idea how long the wait might be. To display the “indeterminate wait” animation, call the setIndeterminate method.

Listing 10.26 shows the full program code.

### Listing 10.26 progressBar/ProgressBarFrame.java

```java
package progressBar;

import java.awt.*;
import java.util.List;

import javax.swing.*;

/**
 * A frame that contains a button to launch a simulated activity, a progress bar, and a text area
 * for the activity output.
 */
public class ProgressBarFrame extends JFrame
{
    public static final int TEXT_ROWS = 10;
    public static final int TEXT_COLUMNS = 40;

    private JButton startButton;
    private JProgressBar progressBar;
    private JCheckBox checkBox;

private JTextArea textArea;
private SimulatedActivity activity;

public ProgressBarFrame()
{
    // this text area holds the activity output
    textArea = new JTextArea(TEXT_ROWS, TEXT_COLUMNS);

    // set up panel with button and progress bar

    final int MAX = 1000;
    JPanel panel = new JPanel();
    startButton = new JButton("Start");
    progressBar = new JProgressBar(0, MAX);
    progressBar.setStringPainted(true);
    panel.add(startButton);
    panel.add(progressBar);

    JCheckBox checkBox = new JCheckBox("Indeterminate");
    checkBox.addActionListener(event ->
    {
        progressBar.setIndeterminate(checkBox.isSelected());
        progressBar.setStringPainted(!progressBar.isIndeterminate());
    });
    panel.add(checkBox);
    add(new JScrollPane(textArea), BorderLayout.CENTER);
    add(panel, BorderLayout.SOUTH);

    // set up the button action

    startButton.addActionListener(event ->
    {
        startButton.setEnabled(false);
        activity = new SimulatedActivity(MAX);
        activity.execute();
    });
    pack();
}

class SimulatedActivity extends SwingWorker<Void, Integer>
{
    private int current;
    private int target;

    /**
     * Constructs the simulated activity that increments a counter from 0 to a
     * given target.
     * @param target the target value of the counter
     */
69    public SimulatedActivity(int t)
70    {
71        current = 0;
72        target = t;
73    }
74
75    protected Void doInBackground() throws Exception
76    {
77        try
78        {
79            while (current < target)
80            {
81                Thread.sleep(100);
82                current++;
83                publish(current);
84            }
85        }
86        catch (InterruptedException e)
87        {
88        }
89        return null;
90    }
91
92    protected void process(List<Integer> chunks)
93    {
94        for (Integer chunk : chunks)
95        {
96            textArea.append(chunk + "\n");
97            progressBar.setValue(chunk);
98        }
99    }
100
101    protected void done()
102    {
103        startButton.setEnabled(true);
104    }
105 }
106 }
```

### 10.5.2 Progress Monitors

A progress bar is a simple component that can be placed inside a window. In contrast, a *ProgressMonitor* is a complete dialog box that contains a progress bar (see Figure 10.42). The dialog box contains a Cancel button. If you click it, the monitor dialog box is closed. In addition, your program can query whether the user has
