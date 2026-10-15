# Host Process

A host process is an executable program that hosts a workflow. It may be a Windows application, a Web application, or a Web service application. A host process interacts with a workflow by using the WorkflowInvoker class and invokes the workflow as a method. The workflow is hosted and run within the host process. You can use Web services in the host process or remoting to enable other applications to communicate with the workflow.

# Activity Data Model

In WF 4, activities store and maintain the data by using the following elements:

+   - Variable: Stores the data in an activity
+   - Argument: Moves the data in and out from an activity and a workflow
+   - Expression: Represents an activity that returns the values used in arguments

# Base Activity Library

The base activity library is a collection of standard actions, known as activities, used to create workflows. The action that an activity implements can be a simple action, such as a delay, or it can be a composite activity that consists of multiple child activities. The activities contained in the base activity library provide functionalities for control flow, state management, event handling, and communicating with applications and services. Each activity has an activity execution context, which represents the execution environment of the activity.

# Custom Activities

In addition to the standard activities available within the base activity library, you can create new activities to meet specific business needs. Creating custom activities may be required to support a particular application that you want to integrate with WF. Custom activities are generally created through attributes and inheritance. You can create two types of custom activities, base and composite. To create a basic custom activity, you need to inherit the Activity class; whereas, to create a custom composite activity, you need to inherit the CompositeActivity class or a derived type.

# Runtime Engine

The runtime engine of WF provides the basic functionality required to execute and manage the workflow lifetime. It interacts with the host process and is responsible for executing each workflow instance. A host process can interact with multiple runtime engines simultaneously, where each engine executes multiple workflow instances. The host process interacts with runtime engine by using any of the following classes:

+   - WorkflowInvoker — Invokes a workflow as a method
+   - WorkflowApplication — Controls the execution of a single workflow instance explicitly
+   - WorkflowServiceHost — Allows message-based interactions between multiple instances of workflows

# Runtime Services

Runtime services provide features to customize the behavior of the workflow runtime. Some of the runtime services available in WF 4.0 are as follows:

+   - Persistence service — Enables you to save or restore the state of a workflow to or from a durable medium. As a workflow can take long time to complete; therefore, multiple workflows running at the same time use a lot of memory. The persistence service enables workflows to be saved for later use.
+   - Tracking services — Enables you to monitor the state of the workflows. This is particularly useful when you have multiple workflows active at the same time (for instance, in a shopping cart application). The tracking services enable you to create applications to monitor your workflows.
+   - Timer service — Manages the timing required by the DelayActivity activity.
+   - Transactions service — Provides the transaction support needed for data integrity.
+   - Threading services — Administers physical threads used to execute workflow instances.