
| ACTIVITY | PROPERTY | VALUE | DESCRIPTION |
|---|---|---|---|
| InvokeMethod | TargetObject | manager | This is an instance of an OrderSystem class. |
|  | MethodName | ValidateOrder | A method on the OrderSystem class |
|  | Result | ValidationErrors | A variable that will be added to the workflow shortly |
|  | Parameters | theOrder | The instance of the Order class created by the GetOrderFromDropFile method above |

![](img/d99870e80390742f93963da7be0b2e61_896_0.png)

## FIGURE 26-15

Next, the processing branches based on whether errors are encountered in the order. If the order is valid, then it is added to a collection for further processing. If, however, there are any validation errors, they are displayed and the workflow ends (see Figure 26-15). Set the properties for these activities as follows:

| ACTIVITY | PROPERTY | VALUE | DESCRIPTION |
|---|---|---|---|
| If | Condition | ValidationErrors.Length > 0 | The condition will return true if any errors were added to the collection by the earlier ValidateOrder call. |
| AddToCollection<T> | TypeArgument | OrderManager.Order | This defines the type of objects stored in the collection. |
|  | Collection | Orders | This is a variable of the workflow that will store the orders. |
|  | Item | theOrder | The item to add to the collection. In this case it is a workflow variable. |
| ForEach<T> | TypeArgument | String | This will iterate over each of the items in the ValidationErrors collection to display them. |
|  | Values | ValidationErrors | This is the collection to iterate over. |
| WriteLine | Text | ValidationError | This is the value of the current iteration in the loop. |
| TerminateWorkflow | Reason | "One or more orders have errors" | This will be available to the calling application to determine why the workflow terminated. |

![](img/d99870e80390742f93963da7be0b2e61_897_0.png)

## FIGURE 26-16

Finally, the orders are simply displayed on the console to confirm they have been processed. This is done with another ForEach<T> activity that writes the order’s information, followed by each of the detail rows in the order (see Figure 26-16). The properties of these activities are defined as follows:

| ACTIVITY | PROPERTY | VALUE | DESCRIPTION |
|---|---|---|---|
| `ForEach<T>` | `TypeArgument` | `OrderManager.Order` | This will iterate over each of the orders in the collection to display them. |
|  | `Values` | `Orders` | This is a workflow variable containing the orders submitted. |
| `WriteLine` | `Text` | `String.Format("Order on {0} by {1} for:", item.OrderDate, item.CustomerName)` | Displays the contents of the order’s header information |
| `ForEach<T>` | `TypeArgument` | `OrderManager.OrderDetails` | This will iterate over the detail rows contained within the submitted order. |
|  | `Values` | `item.Details` | This is the collection of order details within the current order. |
| `WriteLine` | `Text` | `String.Format("{0} {1}(s)", detail.Quantity, detail.ItemName)` | Displays the contents of the fields of each order detail row |

As described above, you will use a number of workflow variables needed to store data during processing. These are described in the following table:

| VARIABLE | TYPE | DESCRIPTION |
|---|---|---|
| theOrder | OrderManager.Order | Will hold the current submitted order |
| Orders | List<Order> | Represents the current queue of orders for processing. Set the default to New List(Of Order) to ensure that the collection is initialized. |
| ValidationErrors | String() | Will hold any validation errors in the current submitted order |

In addition to those variables, an instance of the OrderSystem class will be passed into the workflow as an argument. Open the Arguments pane and add the following item.

| ARGUMENT | TYPE | DESCRIPTION |
|---|---|---|
| manager | OrderManager.OrderSystem | Will hold the object that provides the processing for the loading and validating of the orders |

All that remains is to update the host application. As described above, you will provide an instance of the OrderSystem class to the workflow. This is done in the Main method for the Console application:

```
Shared Sub Main()
    Dim inputs As New Dictionary(Of String, Object)
    'Workflow expects the OrderSystem as parameter
    Dim sys As New OrderManager.OrderSystem
    inputs.Add("manager", sys)
    WorkflowInvoker.Invoke(New FulfilmentWorkflow(), inputs)

    Console.WriteLine("Press ENTER to exit")
    Console.ReadLine()
End Sub
```

Code snippet from Fulfillment

Recall that the input for a workflow is a Dictionary(Of String, Object), and that the key in this dictionary must match the name of an argument in the system — in this case, manager.

Before running the application, you also need to add an application configuration file. This will include a single application setting named dropFilePath that should be set to the location where you will add the XML files.

Run the application and copy an XML file to the monitored directory. After a brief delay, you should see the contents of the order displayed on the console (see Figure 26-17).

![](img/d99870e80390742f93963da7be0b2e61_898_0.png)

FIGURE 26-17

## Building Custom Activities

In addition to the standard activity library, WF supports extensibility through the creation of custom activities. Creating custom activities is a matter of creating a new class that inherits from Activity (or one of the existing child classes). Creating custom activities is the primary means of extending WF. You might use custom activities to simplify a complex workflow, grouping a number of common activities into a single new activity. Alternatively, custom activities can create a workflow that is easier to understand, using terms that are more familiar to the developers and business experts. Finally, custom activities can be used to support software used within the business, such as activities to communicate with a Customer Relationship Management (CRM) or Enterprise Resource Planning (ERP) system.

Creating custom activities with WF 4 is much easier than it was with earlier releases. To create a custom activity, you inherit from Activity, or one of the existing children of Activity, and override the appropriate methods. The most common classes you will inherit from are as follows:

- Activity — The base class. Use only if one of the other following three classes are too specific for your needs.
- CodeActivity — Use when your activity performs some action. You override the Execute method to carry out your action. This activity works synchronously (as opposed to the AsyncCodeActivity below), so the entire activity must complete before the workflow continues.
- AsyncCodeActivity — Similar to CodeActivity, but the work is performed asynchronously. This is the most commonly used class to inherit from when creating custom activities.
- NativeActivity — Use this when your activity needs to interact with the workflow engine itself. For example, the flow control activities inherit from this class.

When defining properties for your custom activities, you do not use the standard types. Instead, you use a generic class to wrap the type. This enables your properties to communicate with the running workflow. There are three wrappers you should use in your activities:

- InArgument(Of type) — Used to wrap a property that will be provided to the workflow
- OutArgument(Of type) — Used to wrap a property that the workflow will expose to the calling code
- InOutArgument(Of type) — Used to wrap a property that will be provided to the workflow, as well as returned

To see how you can easily create a new activity and use it within a workflow, create a new Workflow Console application (CustomActivity). Add a new class (EncryptActivity) to the project for your new activity. This new activity will be used to encrypt a string within a workflow (you'll also be creating an activity to decrypt the text):

```
Imports System.Activities
Imports System.Security.Cryptography
Imports System.Text

Public Class EncryptActivity
    Inherits CodeActivity

    Public Property Input As InArgument(Of String)
    Public Property Password As InArgument(Of String)
    Public Property Output As OutArgument(Of String)

    Protected Overrides Sub Execute(ByVal context As CodeActivityContext)
        Dim aes As New AesCryptoServiceProvider
        Dim hash As New MD5CryptoServiceProvider

        'load the properties from the current workflow context
        Dim plaintext As String = Input.Get(context)
```
