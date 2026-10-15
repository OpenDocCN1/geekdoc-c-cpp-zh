
For the final example, then, you can take the original transactional component and add in a queued element, so that not only does the transfer of money take place, but that fact is also logged to a remote file. Use exactly the same queued component as last time.

Begin by making a clone of TestTransactions called TestQueuedTransactions. Add a reference to Queues and an Imports statement:

```
Imports System.Runtime.InteropServices
```

You also need a new private subroutine:

```
Private Shared Sub LogTransaction(ByVal amount As Decimal, _
    ByVal sourceBank As String, ByVal sourceAccount As String, _
    ByVal destinationBank As String, ByVal destinationAccount As String)
    Dim logger As Queues.IReporter
    Try
        logger =
            CType(Marshal.BindToMoniker("queue:/new:Queues.Reporter"),
            Queues.IReporter)
        logger.Log(String.Format("{0:c} transfered from {1}:{2} to {3}:{4}",
            amount,
            sourceBank, sourceAccount,
            destinationBank, destinationAccount))
        Marshal.ReleaseComObject(logger)
        MessageBox.Show("Message sent")
    Catch ex As Exception
        MessageBox.Show(ex.Message, "Error sending message")
    End Try
End Sub
```

Code snippet from TestQueuedTransactions

This may look similar to the previous queued component example application. Finally, add a call to this subroutine in the Button_Click event handler:

```
Private Sub TransferButton_Click(ByVal sender As System.Object,
    ByVal e As System.EventArgs) Handles TransferButton.Click
    Dim txn As New Transactions.BankTransactions
    Try
        txn.TransferMoney(CDec(Me.TransferField.Text),
            "BankOfWrox", "Professional VB",
            "BankOfMe", "Me")
        LogTransaction(CDec(Me.TransferField.Text),
            "BankOfWrox", "Professional VB",
            "BankOfMe", "Me")
        MessageBox.Show(String.Format("{0:C} transfered from {1} to {2}",
            CDec(Me.TransferField.Text), "BankOfWrox", "BankOfMe"),
            "Transfer Succeeded",
            MessageBoxButtons.OK,
            MessageBoxIcon.Information)
    Catch ex As Exception
        MessageBox.Show(ex.Message, "Transfer failed",
            MessageBoxButtons.OK,
            MessageBoxIcon.Error)
    End Try
End Sub
```

Code snippet from TestQueuedTransactions

Here, you’ve included a queued component in the transaction. It’s been deliberately placed at the beginning to determine whether it genuinely takes part in the two-phase committal. If the transaction fails, then you shouldn’t see any messages come through the queue.

You also need to make a small change to the Reporter component, but you must shut it down via the Component Services Console first. The change is very simple. To ensure that the queued component takes part in the transaction, it must be marked with the Transaction attribute:

```
<InterfaceQueuing(Interface:="Reporter.IReporter"),
Transaction(TransactionOption.Required)>
Public Class Reporter
```

Code snippet from Queues

If you now transfer $500, you'll see the usual “Transfer complete” message box; and if you start up the WroxQueue component, you also see the message box from the queued component (see Figure D-19).

![](img/d99870e80390742f93963da7be0b2e61_1197_0.png)

FIGURE D-19

If you try it again, you see the queued message coming through first, so you know it's OK for valid transfers. What happens if you try to transfer $100? As you know from the earlier example, this will fail, and indeed, you'll see the “Transfer failed” message box from the main component, but not a peep out of the queued component.

## SUMMARY

This appendix looked at creating applications using the classes of System.EnterpriseServices. You first examined transactions and their importance in maintaining data integrity when multiple simultaneous changes may affect your data. Properly applied, transactions can ensure that even with multiple users editing data, your database always reflects the correct data. You also looked at asynchronous processing using MSMQ and queued components. Many scenarios, such as logging or other “background” processes, are better handled using asynchronous code. Queued components make building these asynchronous handlers much easier. Many other aspects of Enterprise Services were beyond the scope of this appendix, including role-based security, object constructors, and more.

## Programming for the Cloud

Can you hear it? Those drums beating in the programming jungle: They’re getting louder and louder. All of the major vendors have begun to offer some sort of “cloud computing” services, and Microsoft is no exception.

This appendix looks at Windows Azure, a new set of tools from Microsoft for creating applications that run within their cloud. This includes the capability to create highly scalable websites, massively parallel computation tools, or some combination of the two. It looks at how creating these applications differs from the way you normally work, and some of the benefits of creating applications that run in the cloud.

### THE RISE OF THE CLOUD

Cloud computing is very much the latest buzzword in computing, but just about every vendor means something slightly different when they use it, and they’re all basically right. However, a few consistent concepts emerge when discussing cloud computing:

- The services are provided by one or more computers in a data center.
- You can easily add new servers, typically with either a Web interface or a configuration option. These new servers are available within a few minutes of the request.
- Any given server might be servicing requests from multiple cloud applications, without any interaction between these applications.
- The developer creating the cloud application is usually constrained, especially in matters of reading and writing data. For example, you cannot directly read and write to the file system, and the choice in databases is limited, as you will see later in this appendix.
- The cost of using the cloud is typically billed based on actual usage, rather than a set rate per server. This is one of the main points that distinguishes cloud computing from a simple data-center-hosted application.

In the case of Windows Azure, your applications run within a virtual machine on a server running within one of Microsoft’s data centers. These virtual machines provide all the services you need to run your application. Adding new “servers” is simply a matter of creating a new copy of your virtual machine. This means that a new server can run your application in a matter of minutes, not days or weeks.

### Cloud Scenarios

There are a number of scenarios in which making use of cloud computing can be highly useful, including the following:

- Websites that have highly variable scaling needs
- As a means of reducing the maintenance cost of a server farm
- Providing a highly scalable parallel processing environment

### Scalability

Some websites have highly variable traffic patterns. For example, a site that sells a product might have higher traffic during peak gift-giving seasons (see Figure E-1).

![](img/d99870e80390742f93963da7be0b2e61_1199_0.png)

FIGURE E-1

One line represents the capacity of a single Web server, in terms of the number of requests it can respond to. The other line represents incoming traffic. From the graph, you can see that the site will have difficulty maintaining good server loads at least three times during the year: in February, May, and December. During these times, the number of people attempting to access the site exceeds the available server capacity. This would lead to slower response times from the site, which would likely lead to visitors going elsewhere.

At this point, you have a few alternatives. You could increase the available server capacity by using more servers. However, this means that you now have the cost of acquiring and maintaining those servers, even though they will remain idle most of the year. In this case, that would mean you would need four times the number of servers to meet the December traffic requirements.

As an alternative, you could use Windows Azure to host your Web application. This enables you to easily add new servers only when they are needed, shutting them down again when they are not. As shown in Figure E-2, this option gives you a closer fit between your needs and the capacity of the servers.

This is one of the main benefits of using a cloud computing service like Azure — you can easily scale your application by adding new servers when needed. You only pay for the computer access you use at any given time.
