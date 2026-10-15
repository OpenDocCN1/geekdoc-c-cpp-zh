# LISTING 6.8 continued

```
page.setColor (Color.green);
page.fillRect (x, y, width, height);
}
else
{
page.setColor (Color.white);
page.drawRect (x, y, width, height);
}
}
}
}
```

# 6.6 Dialog Boxes

A component called a dialog box can be helpful to assist in GUI processing. A dialog box is a graphical window that pops up on top of any currently active window so that the user can interact with it. A dialog box can serve a variety of purposes, such as conveying some information, confirming an action, or allowing the user to enter some information. Usually a dialog box has a solitary purpose, and the user's interaction with it is brief.

> KEY CONCEPT
> A dialog box is a pop-up window that allows brief, specific user interaction to provide information or verify an action.

The Swing package of the Java class library contains a class called JOptionPane that simplifies the creation and use of basic dialog boxes. Figure 6.3 lists some of the methods of JOptionPane.

```
static String showInputDialog (Object msg)
Displays a dialog box containing the specified message and an input text field. The contents of the text field are returned.

static int showConfirmDialog (Component parent, Object msg)
Displays a dialog box containing the specified message and Yes/No button options. If the parent component is null, the box is centered on the screen.

static void showMessageDialog (Component parent, Object msg)
Displays a dialog box containing the specified message. If the parent component is null, the box is centered on the screen.
```

FIGURE 6.3 Some methods of the JOptionPane class