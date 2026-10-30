Building macros consists of selecting actions from a drop-down list and then filling in the action’s arguments (values that provide information to the action). Macros let you choose actions without writing a single line of VBA code. The macro actions are a subset of commands VBA provides. Most people find it easier to build a macro than to write VBA code. If you’re not familiar with VBA, building macros is a great stepping-stone to learning some of the commands available to you while providing added value to your Access applications.

Suppose you want to build a main form with buttons that open the other forms in your application. You can add a button to the form, build a macro that opens another form in your application, and then assign this macro to the button’s Click event. The macro can be a stand-alone item that appears in the Navigation pane, or it can be an embedded object that is part of the event itself (see the “Embedded Macros” section, later in this chapter).

# Creating a macro

A simple way to demonstrate how to create macros is to build one that displays a message box that says “Hello World!” To create a new stand-alone macro, click the Macro button on the Macros & Code group on the Create tab of the Ribbon (shown in Figure 22.1).

# FIGURE 22.1
Use the Macro button on the Create tab to build a new stand-alone macro.

![](bbox=[0.15, 0.58, 0.88, 0.71])

Clicking the Macro button opens the macro builder (shown in Figure 22.2). Initially, the macro builder is almost featureless. The only thing in the Macro Builder is a drop-down list of macro actions.

To the right of the Macro Builder you may see the Action Catalog. There are dozens of different macro actions, and knowing which action to use for a particular task can be an issue. The Action Catalog provides a tree view of all available macro actions and helps you know which action is needed to perform a particular task.

Select MessageBox from the drop-down list in the macro builder. The macro builder changes to display an area where you input the arguments (Message, Beep, Type, and Title) associated with the MessageBox action.

Set the arguments as follows:

+   - Message: Hello World!
+   - Beep: No
+   - Type: None
+   - Title: A Simple Macro