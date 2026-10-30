# The status bar

Keeping your users informed about what’s happening with your application is an important part of building a good user experience. Access provides a SysCmd function that lets you display messages in the status bar (the thin colored bar across the bottom of the screen).

By default, the status bar shows information about the state of the object you’re working on. For example, when you have a form open in Design view, the left side of the status bar reads “Design View.” The status bar also displays whether the Num Lock key is active. Depending on the type of object you have open, the View buttons on the far right of the status bar provide a quick way to switch between views.

Using SysCmd, you can display your own messages on the left side of the status bar. The status bar is a great place to display noncritical messages because it doesn’t require any user interaction (other than reading it, of course).

To show a message in the status bar, use the acSysCmdSetStatus parameter, as shown in the following code:

```
Private Sub cmdHelpText_Click()

    Const sMSG As String = "Hello, World!"

    SysCmd acSysCmdSetStatus, sMSG

End Sub
```

This code displays "Hello, World!" in the status bar, but you can display any string you’d like. However, if the string is longer than Access has space to show, nothing will display. The status bar can also be used to show the user what is happening during a long process. In the following code, the status bar is updated while looping through a large recordset:

```
Private Sub cmdLoop_Click()

    Dim rs As DAO.Recordset
    Dim sSql As String
    Dim lCnt As Long

    sSql = "SELECT * FROM tblLarge;"
    Set rs = CurrentDb.OpenRecordset(sSql, dbOpenSnapshot)
    rs.MoveLast
    rs.MoveFirst

    Do While Not rs.EOF
        lCnt = lCnt + 1
        If lCnt Mod 10 = 0 Then
```