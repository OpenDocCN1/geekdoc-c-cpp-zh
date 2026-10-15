InArgument, InOutArgument, and OutArgument, to determine the direction of data while moving the data in and out of the activity.

# The Flowchart Control Flow Activity

In WF 4.0, a new control flow activity, Flowchart, is introduced to implement loops and conditional branching in workflows. The Flowchart control activity allows you to create flexible workflows in which you can navigate back to previous steps as well as skip steps based on conditions within the workflow. You can add the Flowchart activity into your workflow either by the code or by using the Workflow designer. You can create multiple Flowchart activities in a workflow, but execute only one activity at a time.

# Workflow Activity Model

In WF 4.0, an activity is elementary unit of creating a workflow, which is implemented in the workflow by using the Activity class. The workflow activity model enables you to break complex business processes of a workflow into smaller processes. This ensures reliable flow control with automatic exception handling. You can use the CodeActivity class to add basic custom functionality to your activity.

# Enhancements in Built-In Activity Library

The WF 4.0 activity library contains a set of pre-defined activities that you can use in your workflow. These activities are not intended to be used to create new functionality through inheritance. Some new activities, added to the built-in activity library, are given as follows:

+   - New flow control activities, such as DoWhile, Pick, TryCatch, ForEach, Switch, and ParallelForEach
+   - Activities for manipulating the data, such as Assign
+   - Collection activities, such as AddToCollection
+   - Activities for controlling transactions, such as TransactionScope and Compensate
+   - Messaging activities, such as SendContent and ReceiveReply

Let’s now learn about the components of WF 4.0.

# Describing Components of WF 4.0

WF consists of several components that work together to create a desired workflow. For instance, a custom activity is a component of WF that allows you to define your own activity to be performed in a workflow. With the help of this component you can easily create the workflow-based applications according to your requirement. All the components of WF are given as follows:

+   - Workflows and activities
+   - Host process
+   - Activity data model
+   - Base activity library
+   - Custom activities
+   - Runtime engine
+   - Runtime services

Let’s discuss these components in detail, one by one.

# Workflows and Activities

A workflow is a collection of actions that presents the model of a process. Each action represents an activity. These activities are stored as a model to describe a real world process. A workflow provides a way to describe the order of the execution of a long running process. In Visual Studio 2010, a workflow instance is created and maintained by an in-process runtime engine.