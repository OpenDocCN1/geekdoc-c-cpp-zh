![](bbox=[0.17, 0.13, 0.74, 0.35])

Figure 10.37 The FormatTest program

# Listing 10.20 textformat/FormatTestFrame.java

```
```java
 1 package textformat;
 2
 3 import java.awt.*;
 4 import java.net.*;
 5 import java.text.*;
 6 import java.util.*;
 7
 8 import javax.swing.*;
 9 import javax.swing.text.*;
10
11 /**
12  * A frame with a collection of formatted text fields and a button that displays the field values.
13  */
14 public class FormatTestFrame extends JFrame
15 {
16    private DocumentFilter filter = new IntFilter();
17    private JButton okButton;
18    private JPanel mainPanel;
19
20    public FormatTestFrame()
21    {
22       JPanel buttonPanel = new JPanel();
23       okButton = new JButton("Ok");
24       buttonPanel.add(okButton);
25       add(buttonPanel, BorderLayout.SOUTH);
26
27       mainPanel = new JPanel();
28       mainPanel.setLayout(new GridLayout(0, 3));
```
```

(Continues)