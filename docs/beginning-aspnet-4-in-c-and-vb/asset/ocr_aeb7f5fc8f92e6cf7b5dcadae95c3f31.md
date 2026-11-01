The WriteLine activity includes a Text property that you can set either on the design surface itself by simply entering text inline, or by displaying the property grid. Later in this chapter, we show you how to define your custom activities to use this same behavior.

The Text property is not just a simple string — it's actually defined as an argument type that can use an expression as its source. Expressions are evaluated at runtime to yield a result, and it is this textual result that is used as the input to the WriteLine activity. To enter a simple text expression, you must use double quotation marks — so if you are following along with this in Visual Studio, type "Hello World" into the Text property. If you omit the quotation marks, you will receive a compiler error, as without quotation marks this is not a legal expression.

If you build and run the program, you will see the output text on the console. When the program executes, an instance of the workflow is created in the Main method, which uses a static method of the WorkflowInvoker class to execute the instance. The code for this example is available in the 01_HelloWorld solution.

The WorkflowInvoker class is new to Workflow 4, and it lets you synchronously invoke a workflow. There are two other methods of workflow execution that execute workflows asynchronously, which you'll see later in this chapter. Synchronous execution was possible in Workflow 3.x but was somewhat more difficult to set up, and there was a lot more overhead.

The synchronous nature of WorkflowInvoker makes it ideal for running short-lived workflows in response to some UI action — you could use a workflow here to enable or disable some elements of the UI. While it was possible to do this in Workflow 3.x, it was also more difficult to synchronously execute a given workflow instance.

# ACTIVITIES

Everything in a workflow is an activity, including the workflow itself. The workflow is a specific type of activity that typically allows other activities to be defined within it — this is known as a composite activity, and you'll see other composite activities later in this chapter. An activity is just a class that ultimately derives from the abstract Activity class.

The class hierarchy is somewhat deeper than that defined for Workflow 3.x, and the main classes are defined in Figure 44-3.

![](bbox=[0.15, 0.86, 0.85, 0.92])

FIGURE 44-3

The Activity class is the root for all workflow activities and typically you will derive custom activities from the second tier. To create a simple activity like the WriteLine activity previously mentioned, you would derive from CodeActivity, as this class has just enough functionality for your write line