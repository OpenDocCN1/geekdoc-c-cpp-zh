Let’s learn how to handle runtime errors in WF 4.0.

# Handling Runtime Errors

Till now, you have learned about the workflow and the activities that are used to create the workflows. Suppose that you have created a workflow and at the time of executing the workflow it throws an error. This error can easily be handled and rectified in a small workflow, on the other hand, if your workflow is complex and contain number of various activities then finding and rectifying that error might be difficult. Therefore, WF 4.0 provides various mechanisms to handle the runtime errors. These mechanisms are given as follows:

+   - Exceptions – Enables you to use the TryCatch activity to handle exceptions that are raised during the execution of workflows. You can also rethrow the exception by using the Rethrow activity. After the execution of the activities included in the Try and Catch sections, the activities of the Finally section are executed.
+   - Transactions – Provides the TransactionScope activity to use transactions in a workflow.
+   - Compensation – Provides the compensation activities, such as CompensableActivity, Compensate, and Confirm, to compensate the previously completed task or a subsequent failure.
+   - Cancellation of Workflows – Offers the CancellationScope activity, the CompensableActivity activity, or custom activities that provide cancellation logic.

Let’s now learn how to host workflows in WF 4.0.

# Hosting Workflows

Hosting is the process of sharing your workflow with other users so that they can use your workflow in their application. You can host you workflow in a host application and if your workflow suits the requirements of the users can use your workflow from the host application. WF 4.0 provides three classes to host workflows. These classes are as follows:

+   - WorkflowInvoker – Invokes a workflow as its method
+   - WorkflowApplication – Consists of control flow activities, bookmark resumption, and persistence
+   - WorkflowServiceHost – Hosts the workflows and allows sending and receiving messages among various instances of workflows

Let’s explore these classes in the following sections.

# The WorkflowInvoker Class

The WorkflowInvoker class belongs to the System.Activities namespace. The class hierarchy of the WorkflowInvoker class is given as follows:

```
system.Object
System.Activities.WorkflowInvoker
```

You can invoke a workflow or an activity by using the Invoke() method of the WorkflowInvoker class. The following code snippet shows the use of the Invoke() method of the WorkflowInvoker class:

```
Activity myworkflow = new WriteLine(Text = "WELCOME");
workflowInvoker.Invoke(myworkflow);
```

In the preceding code snippet, a WriteLine activity (myWorkflow) is created. Then, the myWorkflow activity is passed as a parameter to the Invoke() method of the WorkflowInvoker class.

You can pass the data into a workflow by using a list of input parameters, as shown in the following code snippet:

```
Activity myworkflow = new WriteLine();
Dictionary<string, object> inputdata = new Dictionary<string, object>();
inputdata.Add("Text", " WELCOME ");
workflowInvoker.Invoke(myworkflow, inputdata);
```

In the preceding code snippet, a WriteLine activity is created and the value of its Text argument is provided by the dictionary of input parameters. You can also obtain the data from a workflow through its output parameters.