# Setting property values

You use the CurrentDb object’s CreateProperty and Properties.Append methods to add each of these properties. In most cases, unless the property has already been set in the Access Options dialog box, the property hasn’t been appended to the database’s Properties collection. You must make sure the property exists before trying to set its value in code. The following function sets the value of a startup property, creating and appending the property to the Properties collection if the property doesn’t exist:

```
Public Function SetStartupProperty(sPropName As String, _
 ePropType As DAO.DataTypeEnum, vPropValue As Variant) As Boolean

Dim db As DAO.Database
Dim prp As DAO.Property
Dim bReturn As Boolean

Set db = CurrentDb
On Error Resume Next
Set prp = db.Properties(sPropName)

If prp Is Nothing Then
Set prp = db.CreateProperty(sPropName, ePropType, vPropValue)

If prp Is Nothing Then
bReturn = False
Else
 db.Properties.Append prp
 bReturn = True
End If
Else
 prp.Value = vPropValue
 bReturn = True
End If

SetStartupProperty = bReturn

End Function
```

Using SetStartupProperty() is quite easy. You must know the exact property name and data type of the property before invoking SetStartupProperty(). The following subroutine demonstrates how to set a startup property with SetStartupProperty():

```
Sub ChangeAppTitle()

Dim bSuccess As Boolean

bSuccess = SetStartupProperty("AppTitle", dbText, "My Application")

If bSuccess Then
```