# USING THE COMPENSATING TRANSACTION MODEL

Although Table 11-8 summarizes the activities related to transaction handling, it's difficult to imagine how the compensating transaction pattern works in practice. Because it is an essential part of WF 4.0, understanding the concepts behind helps you develop more robust workflows.

Let's create an example that helps you understand how this pattern works with WF 4.0. This example also demonstrates error-handling concepts through a TryCatch activity.

# The ConferenceWorkflow Example

This example will demonstrate a very simplified case of a conference registration when you also arrange travelling and book a hotel reservation.

Create a new Workflow Console Application, and name it ConferenceWorkflow. Drag and drop a TryCatch activity to the design surface of Workflow, and then a Sequence activity to the Try block. Set its DisplayName to Conference Preparations. Add a WriteLine activity to Conference Preparations with the Text property set to "Conference preparations completed". Click the "Add an activity" to the Finally block, and drop a WriteLine activity with the "Conference preparations completed" text. Click the Conference Preparations link of the Try block.

Figure 11-16 shows the workflow you've created.

As you expect, when you run this workflow by pressing Ctrl+F5, it generates the following output:

> Conference preparations started
Conference preparations completed

Add a Parallel activity to Conference Preparations below WriteLine and set its DisplayName to "Registration and Travelling". Drop two Compensable activities to the Parallel activity and set their DisplayName to "Registration" and "Travelling", with a Sequence property to the body of Registration, and one other to the body of Travelling, respectively. Drop a WriteLine to the Sequence with Registration and set it to "(Body) Pay $1,500 registration fee.\ Add a Delay after this WriteLine with its Duration to TimeSpan.FromSeconds(2).

Add a WriteLine to the Sequence in Travelling with Text set to "(Body) Pay $1,000 for travelling and hotel", and then a Delay with duration set to TimeSpan.FromSeconds(1).

Now, the Registration and Travelling activities should look like Figure 11-17.

![](bbox=[0.598, 0.318, 0.928, 0.553])

Figure 11-16: The TryCatch activity of the ConferenceWorkflow example