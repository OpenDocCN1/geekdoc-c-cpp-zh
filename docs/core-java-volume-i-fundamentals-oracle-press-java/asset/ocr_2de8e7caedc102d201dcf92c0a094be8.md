![](bbox=[0.27, 0.091, 0.73, 0.327])

**Figure 11.26** A tooltip

In Swing, you can add tooltips to any JComponent simply by calling the setToolTipText method:

```
```
exitButton.setToolTipText("Exit");
```
```

Alternatively, if you use Action objects, you associate the tooltip with the SHORT_DESCRIPTION key:

```
```
exitAction.putValue(Action.SHORT_DESCRIPTION, "Exit");
```
```

# javax.swing.JToolBar 1.2

+   - JToolBar()
+   - JToolBar(String titleString)
+   - JToolBar(int orientation)
+   - JToolBar(String titleString, int orientation)

constructs a toolbar with the given title string and orientation. orientation is one of SwingConstants.HORIZONTAL (the default) or SwingConstants.VERTICAL.