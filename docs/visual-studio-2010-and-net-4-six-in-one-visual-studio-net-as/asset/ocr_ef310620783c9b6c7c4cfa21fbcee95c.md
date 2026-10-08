# Using Expressions

The properties of WriteLine and Assign are a great representation of using arguments and variables in expressions. You can see strange constructs using the Get method of workflow arguments and variables like these:

```
To = new OutArgument<String>(temp)
//...
Value = new InArgument<string>(ctx) => "Message: " + Message.Get(ctx)
//...
Text = new InArgument<string>(ctx) => temp.Get(ctx)
```

To get the actual data from a Variable instance, you must use the Get method. The workflow itself does not store any data elements; you must obtain the data from the context of a concrete workflow instance. This is why lambda expressions in the early snippet sense. The ctx expression parameter is an instance of the ActivityContext class. You must pass the context to the Get method of variable to extract the value of.

The properties of the Activity class are actually workflow parameters that can be represented by InArgument<T> or OutArgument<T> instances. The Text property of WriteLine and Value property of Assign are input arguments, while the To property of Assign is an output argument.

Be sure to put the entire expression into the constructor of InArgument or OutArgument. If you'd write the following

```
Value = "Message: " + new InArgument<string>(ctx) => Message.Get(ctx)
```

instead of the following

```
Value = new InArgument<string>(ctx) => "Message: " + Message.Get(ctx)
```

the output would be

```
Message: System.Activities.InArgument`1[System.String]
```

instead of

```
Message: Hello from WF 4.0
```

# WORKFLOW ARCHITECTURE

By now, you have seen several examples of using the workflow designer to create a workflow, and you have also learned that you can define code-only workflows. Several concepts were also mentioned, such as workflow instances, activities, variables, arguments, workflow persistence, and so on.

This section provides an overview of the workflow architecture so that you can understand how these concepts fit into the entire picture. Figure 11-13 shows an overview of this architecture with its essential elements.