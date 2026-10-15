➢ **Flowchart activities** — These activities are used in flowchart-style workflows and allow for the organization of the steps, simple decisions, and other stages.

| ACTIVITY | DESCRIPTION |
|---|---|
| Flowchart | This activity is used to create a flowchart workflow. It is a container for all the steps involved in the workflow. |
| FlowDecision | A simple If statement within a flowchart workflow. This is used to control the actions of a workflow based on a condition. |
| FlowSwitch | A switch statement within a flowchart workflow. This works similar to the VB case statement in that you have multiple cases that work based on the assigned condition. You also define a default condition if none of the cases apply. |

# A Less Simple Workflow

To see a few of these activities together, create a new Workflow Console Application named Fulfillment. This will be used to create part of a workflow for an order fulfillment application. The workflow will collect an XML file from a directory on disk, validate it using a few simple rules, and add it to a collection representing the order queue. Other workflows might then retrieve items from this collection for actual processing. Figure 26-13 shows the final workflow.

As you can see from the figure, the workflow is a flowchart consisting of four stages. The DisplayName property of each of these stages has been set to better describe the contents of the stage. As you would expect, this is invaluable in improving the understanding of the workflow when you come back to it later (or try to explain it to end users). The basic outline of the workflow is as follows:

![](bbox=[0.557, 0.283, 0.932, 0.588])

**FIGURE 26-13**

+   ➢ The workflow begins a loop to monitor a directory for XML files. This file will represent an order, with one or more details. This is a DoWhile activity.
+   
+   ➢ Once an order is received, a few simple validations are performed by calling a method on a .NET class. This is an InvokeMethod activity.
+   
+   ➢ If the order is valid, it is added to a collection for later processing. If not, the validation errors are displayed and the workflow completes. This is an If activity.
+   
+   ➢ To demonstrate additional processing, the orders collection is simply displayed to the console. Of course, in a real application, this stage would send the orders on to another application for actual fulfillment and shipping. This is a ForEach<T> activity.

Before you begin building the workflow, there are some helper classes that you need to build. These represent an order, an order detail line, and a manager class for processing the order. Add a new Class Library project to the solution, named **OrderManager**. This has three classes: Order, OrderDetail, and OrderSystem.

The Order class represents an order in the system. For this example, it consists of a few properties, including the collection of order details:

```
Public Class Order
    Public Property OrderID As Integer
    Public Property OrderDate As Date
    Public Property CustomerName As String
    Public Property ShipAddress As String
```