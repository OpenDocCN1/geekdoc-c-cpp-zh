```
Loop

daRs.Close
Set daRs = Nothing
Set daDb = Nothing

End Sub
```

In this example, if both BOF and EOF are True, a message is printed and the procedure is exited. If there are records, the code loops through them forward then backward, printing as it goes. The Do Until block of statements is a common way to loop through a recordset.

# Counting records

It's often very useful to know how many records are in a recordset before beginning operations that may take a long time. A user may unwisely select criteria that return too many records to handle efficiently, and you may want your code to alert them before processing a large recordset. Fortunately, Recordset objects provide a RecordCount property that tells you exactly how many records are present in the recordset. The following UseRecordCount subroutine uses the RecordCount property to display the total records as the recordset is processed:

```
Public Sub UseRecordCount()

Dim adRs As ADODB.Recordset
Dim lCnt As Long

Set adRs = New ADODB.Recordset
adRs.ActiveConnection = CurrentProject.Connection
adRs.CursorType = adOpenStatic

adRs.Open "SELECT * FROM tblCustomers;"

Do While Not adRs.EOF
    lCnt = lCnt + 1
    Debug.Print "Record " & lCnt & " of " & adRs.RecordCount
    adRs.MoveNext
Loop

adRs.Close
Set adRs = Nothing

End Sub
```

RecordCount is a convenient way to determine whether a recordset contains any records at all. The only issue with RecordCount is that, on large recordsets, RecordCount penalizes performance. The Recordset object actually counts the number of records it contains, halting execution until the count is complete.