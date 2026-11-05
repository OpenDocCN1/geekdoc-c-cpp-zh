7. Now add the “Send Message” button handler in the parent form by adding following code in the Form1 class.

```
private void GetChildMessage(object sender, System.EventArgs e)
{
    MessageBox.Show(mdlg.Msg);
}
```

8. Add the declaration in the beginning of the Form1 class.

```
private MsgDlg mdlg; // child modeless dialog
```

9. Add a button to the Form1 class. Name the button "btnShowMsgDlg". Give it a text property of "Show Message Dialog". Type the following code in the "Show Message Dialog" handler.

```
private void btnShowMsgDlg_Click(object sender, System.EventArgs e)
{
    System.EventHandler pDel = new system.EventHandler
        (this.GetChildMessage);
    // delegate to GetChildMessage
    mdlg = new MsgDlg(pDel);
    mdlg.Show();
}
```

![](bbox=[0.12, 0.7, 0.88, 0.9])

Fig. 20.6.4 Dialog box window