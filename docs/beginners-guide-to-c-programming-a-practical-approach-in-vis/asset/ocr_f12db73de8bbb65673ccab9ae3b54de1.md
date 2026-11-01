2. Place a NotifyIcon and a ContextMenuStrip on the form. As you drag&drop these elements on the form, you will see that they do not appear on the form. It is because these elements operate in the background and not displayed to the user. After drag&drop operations, you will see these elements below the form design pane:

![](bbox=[0.17, 0.26, 0.86, 0.55])

Figure 5.63. NotifyIcon and ContextMenuStrip elements of the form

3. Click on the contextMenuStrip1 menu (as shown in Figure 5.63) and then it will temporarily appear on the form for entering a right-click menu as in Figure 5.64. Let's insert an Exit item for this example as shown in Figure 5.65.

4. We will now set the action the Exit menu will perform. For this, double-click on the Exit item so that its event handler method ExitToolStripMenuItem_Click(...) will be created in the editor as shown in Figure 5.66.

5. Add the code line Application.Exit(); inside this event handler, which will cause the application to quit when executed:

```
private void exitToolStripMenuItem_Click(object sender,
EventArgs e)
{
    Application.Exit();
}
```

Code 5.18