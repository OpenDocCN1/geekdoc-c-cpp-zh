In some respects, once you have a basic understanding of event-driven programming, the rest is just detail. There are many types of components you can use that produce many types of events that you may want to acknowledge. But they all work in the same basic way. They all have the same core relationships to one another.

The following sections introduce some more components and present examples of GUI-based programs that allow true user interaction.

# SELF-REVIEW QUESTIONS (see answers in Appendix N)

+   - SR 4.30 What is the relationship between an event and a listener?
+   - SR 4.31 Can we add any kind of listener to any component? Explain.

# 4.8 Buttons

The PushCounter program shown in Listing 4.10 presents the user with a single push button (labeled “Push Me!”). Each time the button is pushed, a counter is updated and displayed.

# LISTING 4.10

```
//*******************************************************************
//  PushCounter.java      Author: Lewis/Loftus
//
//  Demonstrates a graphical user interface and an event listener.
//*******************************************************************

import javax.swing.JFrame;

public class PushCounter
{
    //---------------------------------------------------------------
    //  Creates the main program frame.
    //---------------------------------------------------------------
    public static void main (String[] args)
    {
        JFrame frame = new JFrame ("Push Counter");
        frame.setDefaultCloseOperation (JFrame.EXIT_ON_CLOSE);
```