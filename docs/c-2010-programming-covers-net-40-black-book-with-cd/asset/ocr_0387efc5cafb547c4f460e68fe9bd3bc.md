# # In Depth

Windows Workflow Foundation (WF) is a Microsoft technology for defining, executing, and managing workflows. A workflow in WF consists of a sequence of connected steps, where each step represents an activity to be performed by your application. WF consist sequential and state machine workflows. A sequential workflow runs from beginning to end, with the workflow engine initiating each step; whereas, a state machine workflow represents a set of states, transitions, and actions. One state is denoted as the start state, and then, based on external events and user interactions, a transition can be made to another state. The state machine can have a final state that determines the end of the workflow. Workflows use a declarative model of writing programs by linking together pre-defined activities rather than an imperative programming model of writing each line of code.

WF was released with .NET Framework 3.0 in 2006, and then updated in .NET Framework 3.5. In .NET Framework 4.0, the support for WF has been enhanced with many new features, such as flowchart and workflow activity model. WF consists of various templates to create workflows, activities to define logic and control flow, and a runtime engine to execute a WF application. Workflow projects are not complete applications in themselves, but they constitute an application, and require a host for running the workflow. Moreover, WF provides various services and features that are required to write the application logic. It also provides the declarative framework for building application and service logic; thereby, enabling you to handle asynchronous and parallel tasks as well as other complex processing.

In this chapter, you learn about the various new features as well the components of WF 4.0. Next, you learn about the activities that are used to create workflows. You also learn about the various types of workflows in WF 4.0. In addition, you learn about the built-in and bookmark activities. Finally, you learn about handling errors and hosting workflow in an application.

Let's start with the new features of WF 4.0.

# ## Listing New Features of WF 4.0

In WF 4.0, you can easily create, execute, and maintain workflows as well as implement new functionalities in your workflows. WF 4.0 helps you in creating the workflows in less time and without much efforts. Some new features in WF 4.0 are as follows:

+   - Improved workflow designer
+   - Enhancements in data flow model
+   - The Flowchart control flow activity
+   - Workflow activity model
+   - Enhancements in built-in activity library

Let’s discuss these features one by one.

# ### Improved Workflow Designer

One of the most visible areas of improvement in WF 4.0 is workflow designer, which is built on Windows Presentation Foundation (WPF). Workflow Designer now supports complex workflows and provides easier mechanisms to create custom activities. You can use Extensible Application Markup Language (XAML) to define the appearance of your activities and the way the activities interact with users in a visual designed environment. In addition, you can re-host the workflow designer in your applications to enable other users to easily view and interact with your workflows. Re-hosting workflow designer also provides a customized user experience for workflow design.

# ### Enhancements in Data Flow Model

The data flow model defines inputs and outputs of a given activity, manages data, and improves performance of the workflow at runtime. WF 4.0 provides two options, variables and arguments, for data storage and data flow. You can use variables to store the data in an activity. You can also use some specialized arguments, such as