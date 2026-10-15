Let’s explore activities in the context of WF.

# Exploring Activities

In WF, units of work are contained in the form of activities. These activities provide facilities for flow control, exception handling, data persistency, loading or unloading workflows, tracking, and transaction flow. You can implement these activities using the following types:

+   - Activity – Assembles the pre-existing activities to create units of work for executing workflows in the WF environment
+   - CodeActivity – Handles execution logic in the managed code by using the CodeActivityContext class
+   - AsyncCodeActivity – Handles execution logic to implement asynchronous tasks in a workflow
+   - NativeActivity – Provides access to the runtime functionalities, such as creating bookmarks and invoking asynchronous tasks, by using the NativeActivityContext class

Let’s now explore the types of workflows in WF 4.0.

# Describing Types of Workflows

Workflows are a collection of activities that are to be performed in a sequence. In WF 4.0, there are two types of workflows Flowchart and Procedural. The flowchart workflow helps you to create workflows using the common flowchart elements. A flowchart is a common standard to design programs. In WF, the Flowchart activity is generally used to implement a non-sequential workflow, and occasionally it implements sequential workflows incase the FlowDecision nodes are not used in the flowchart. The Flowchart activity contains a collection of flow nodes that are inherited from the FlowNode class. A flowchart can contain the following types of nodes or elements:

+   - FlowStep – Executes activities of a flowchart in a sequence
+   - FlowDecision – Shows the execution on the basis of a Boolean condition. It is similar to the If construct.
+   - FlowSwitch – Shows the execution on the basis of an exclusive switch. It is similar to the Switch construct.

On the other hand, the procedural workflow helps you to create workflows using basic and sequential execution standards. In WF, procedural workflows use flow control constructs, such as While, Switch, ForEach, and If, to execute activities. These flow control constructs are similar to those found in procedural languages. Procedural workflows can also contain other flow control activities, such as Flowchart and Sequence.

Now, let’s learn about built-in activities in brief.

# Exploring Built-in Activities

In WF 4.0, there are certain built-in activities that help you in defining the workflow of your applications. You can use the built-in activities in all the workflow applications. These activities are divided into the following categories:

+   - Control Flow – Controls the flow of execution in a workflow
+   - Flowchart – Controls the execution and branching in a flowchart
+   - Messaging – Allows workflows to send and receive the Windows Communication Foundation (WCF) messages
+   - Runtime – Implements the data persistency and workflow termination processes in workflow applications
+   - Primitives – Manages variables and schedules workflows for execution
+   - Transaction – Performs data transactions, compensation, and cancellation
+   - Collection – Allows you to work with collection objects in a workflow, such as adding and removing items from a collection or clearing a collection
+   - Error Handling – Implements error handling and recovery
+   - Migration – Migrates workflows from previous versions of WF to the current version

Table 28.1 describes the control flow activities: