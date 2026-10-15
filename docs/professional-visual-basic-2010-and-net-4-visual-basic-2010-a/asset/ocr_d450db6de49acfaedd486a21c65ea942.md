What you are doing here is building a list of calculations. When you’re finished, you select the first one in the list. Let’s take a look at that subroutine AddObject:

```
Private Sub AddObject(ByVal strName As String, ByVal strObject As String)
    cmbCalculation.Items.Add(strName)
    mnObject = mnObject + 1
    ReDim Preserve mstrObjects(mnObject)
    mstrObjects(mnObject - 1) = strObject
End Sub
```

The preceding code segment adds the calculation name to the combo box, and its ProgID to an array of strings. Neither of these is sorted, so you get a one-to-one mapping between them. Check out what happens when you select a calculation via the combo box:

```
Private Sub cmbCalculation_SelectedIndexChanged(ByVal sender As System.Object,
    ByVal e As System.EventArgs) _
    Handles cmbCalculation.SelectedIndexChanged

    Dim intIndex As Integer
    Dim bEnabled As Boolean
    intIndex = cmbCalculation.SelectedIndex
    mtypCalc = Type.GetTypeFromProgID(mstrObjects(intIndex))
    If (mtypCalc Is Nothing) Then
        mobjcalc = Nothing
        bEnabled = False
    Else
        mobjcalc = Activator.CreateInstance(mtypCalc)
        bEnabled = True
    End If
    txtInput.Enabled = bEnabled
    btnAdd.Enabled = bEnabled
    btnCalculate.Enabled = bEnabled
    btnReset.Enabled = bEnabled
End Sub
```

There are two key calls in this example. The first is to Type.GetTypeFromProgID. This takes the incoming ProgID string and converts it to a Type object. This process either succeeds or fails; if it fails, then you disable all the controls and let the user try again. If it succeeds, however, then you create an instance of the object described by the type. You do this in the call to the static method Activator.CreateInstance().

For this example, assume that the user has selected a calculation that you can successfully instantiate. What next? The user enters a number and clicks the Add button on the form:

```
Private Sub btnAdd_Click(ByVal sender As System.Object, _
    ByVal e As System.EventArgs) Handles btnAdd.Click
    Dim objArgs() As Object
    objArgs = New Object(0) {CDbl(txtInput.Text)}
    mtypCalc.InvokeMember("AddInput", BindingFlags.InvokeMethod, _
    Nothing, mobjCalc, objArgs)
    txtInput.Text = ""
End Sub
```

The important call here is to the InvokeMember() method. Let’s take a closer look at what is going on. Five parameters are passed into the InvokeMember() method:

+   - The first parameter is the name of the method that you want to call: AddInput in this case. Therefore, instead of going directly to the location of the routine in memory, you ask the .NET runtime to find it for you.