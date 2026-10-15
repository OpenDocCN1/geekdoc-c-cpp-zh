
**4.** Note the current balance and determine whether you can afford to transfer the amount asked for. If not, raise an exception:

```
```vb
'check for overdrafts
    If amount > currentValue Then
        Throw New ArgumentException("Attempt to overdraft account")
    End If
```
```

![](img/d99870e80390742f93963da7be0b2e61_1185_0.png)

**5.** Otherwise, subtract the amount and update the table accordingly:

```
```vb
'otherwise, we're good to withdraw
SQL = _
    String.Format("UPDATE Accounts SET Amount = {0} WHERE Name = '{1}'", _
    currentValue - amount, account)
cmdUpdate = New SqlCommand(SQL, conn)
cmdUpdate.ExecuteNonQuery()
```
```

![](img/d99870e80390742f93963da7be0b2e61_1185_1.png)

**6.** Close the exception handler and the database:

```
```vb
Catch ex As Exception
        Throw New DataException("Error withdrawing", ex)
    Finally
        If Not conn Is Nothing Then
            conn.Close()
        End If
    End Try
End Sub
```
```

![](img/d99870e80390742f93963da7be0b2e61_1185_2.png)

## The Second Half of the Transaction

The second half of the transaction is similar, except that the failure conditions are slightly different. First, the code stipulates that you can’t transfer less than $50. Second, a bug has been included such that an attempt to transfer a negative amount will cause a divide by zero. (You’ll see why this was added in a moment.) Here’s the code:

```
```vb
Private Sub Deposit(ByVal bank As String, _
    ByVal account As String, _
    ByVal amount As Decimal)
    Dim ConnectionString As String
    Dim SQL As String
    Dim conn As SqlConnection = Nothing
    Dim cmdCurrent As SqlCommand
    Dim currentValue As Decimal
    Dim cmdUpdate As SqlCommand
    ConnectionString = My.Settings.Item(bank).ToString
    SQL = String.Format("SELECT Amount FROM Accounts WHERE Name = '{0}'", _
        account)
    If amount < 0 Then
        amount = amount / 0
    ElseIf amount < 50 Then
        Throw New ArgumentException("Value of deposit must be greater than $50")
    Else
        Try
            conn = New SqlConnection(ConnectionString)
            conn.Open()
            'get the current value
            cmdCurrent = New SqlCommand(SQL, conn)
            currentValue = CDec(cmdCurrent.ExecuteScalar())
```
```

```
SQL = _
    String.Format("UPDATE Accounts SET Amount = {0} WHERE Name = '{1}'", _
    currentValue + amount, account)
    cmdUpdate = New SqlCommand(SQL, conn)
    cmdUpdate.ExecuteNonQuery()
Finally
    If Not conn Is Nothing Then
        conn.Close()
    End If
End Try
End If
End Sub
```

Code snippet from Transactions

The business logic component is complete. Let’s see how you can bring it under the control of Enterprise Services. First, of course, you need to build your DLL. Select Build Transactions from the Build menu.

Why was the divide by zero error included? This gives you a chance to see what happens to the transaction when an exception occurs in your code. The transaction will automatically fail and roll back, which means that your data will still be in a good state at the end.

## Registering Your Component

Because the Enterprise Services infrastructure is COM-oriented, you need to expose the .NET component as a COM component, and register it with Component Services. Component Services handles all transaction coordination; that is, Component Services tracks any changes and restores the data should the transaction fail. First, some changes to the component are needed to enable this COM interaction. Prepare to take a trip down memory lane.

All COM components must have a GUID (globally unique identifier) that uniquely identifies it to the COM infrastructure. This was done for you in Visual Basic 6.0, but .NET requires you to add a value. In addition, your component needs an attribute to make it visible to COM. You can set both of these in the Assembly Information dialog. Double-click My Project in the Solution Explorer. On the Application page, click Assembly Information. There should already be a GUID assigned to your component. Check the option Make Assembly COM-Visible, as shown in Figure D-9. This makes all of the Public types accessible to COM.

![](img/d99870e80390742f93963da7be0b2e61_1186_0.png)

You should also update the Assembly Version fields as you make changes to the component.

> Chapter 28 contains more information about strong names and assemblies.

The problem is that the assembly is a private assembly. In order to make it available to the transaction framework, it needs to be a shared assembly. To do this, give the assembly a cryptographically strong name, generally referred to as its strong name.

Cryptographically strong means that the name has been signed with the private key of a dual key pair. This isn’t the place to go into a long discussion about dual-key cryptography, but essentially a pair of keys is generated, one public and one private. If something is encrypted using the private key, it can only be decrypted using the public key from that pair, and vice versa. It is therefore an excellent tool for preventing

tampering with information. If, for example, the name of an assembly were to be encrypted using the private key of a pair, then the recipient of a new version of that assembly could verify the origin of that new version, and be confident that it was not a rogue version from some other source. This is because only the original creator of the assembly retains access to its private key.

## Giving the Assembly a Strong Name

You now need to ensure that your assembly uses the strong name. You can create a new strong name file, or assign an existing strong name file on the Signing tab of the Project Properties (see Figure D-10).

![](img/d99870e80390742f93963da7be0b2e61_1187_0.png)

## Registering with Component Services

Once you’ve built the DLL again, you can run RegSvcs to register the DLL with Component Services (see Figure D-11). RegSvcs is a command-line tool, so start a Windows Command Prompt. You will find the RegSvc.exe tool in the directory %windir%\Microsoft .NET\Framework\v4.0.21006 directory. To register a DLL, simply pass the full path of the DLL on the command-line:

```
regsvcs.exe {path to DLL}\transactions.dll
```

To unregister a DLL, include the /u parameter on the command-line.

![](img/d99870e80390742f93963da7be0b2e61_1187_1.png)

> Running RegSvcs.exe requires administrative permissions. Therefore, when running under Windows Vista or Windows 7, you should start the command prompt by selecting “Run As Administrator.” Otherwise, RegSvcs will fail when run.

RegSvcs does a few things at this point. It creates a COM type library for the DLL, which enables it to communicate with COM, and it creates a COM+ application for the component.

## The Component Services Console

The Component Services Console is the control interface for Component Services. This is an MMC snap-in, which you can find by selecting Control Panel ➤ Administrative Tools ➤ Component Services (see Figure D-12). If the Component Services tool is not available, you can also run it by selecting Run from the start menu/orb and running c:\windows\system32\comexp.msc.

![](img/d99870e80390742f93963da7be0b2e61_1188_0.png)

# FIGURE D-12

You should be able to find the sample under COM+ Applications. A COM+ application is a set of related COM+ components that have been packaged together. RegSvcs creates a new application for every component that it registers. If you want to bundle together a series of components from separate DLLs, you can do so, but only by creating a new application via the Component Services Console (right-click COM+ Applications and then select New). You’ll explore the console a little more as you go on.

Now you need a test application. More important, you need to tell Component Services that you’re interested in transactions.

## Test Application

Create a Windows Application project called TestTransactions and a very simple form (see Figure D-13).

![](img/d99870e80390742f93963da7be0b2e61_1188_1.png)

# FIGURE D-13

The text field is called TransferField and the command button is called TransferButton. In order to access the transactional component, add references to a couple of DLLs. First, add a reference to the transactional component DLL itself. You’ll need to browse for this, as it isn’t currently in the global assembly cache. Second, in order to access the objects in this DLL, you also need to make the application aware of the System.EnterpriseServices assembly, so add a reference to that as well. Having done that, it’s time to import Transactions into the application:

```
Imports Transactions
```

Here’s the code behind the TransferButton button:

```
Private Sub TransferButton_Click(ByVal sender As System.Object, _
    ByVal e As System.EventArgs) Handles TransferButton.Click
    Dim txn As New BankTransactions
    Try
        txn.TransferMoney(CDec(Me.TransferField.Text),
        "BankOfWrox", "Professional Visual Basic 2010",
```
