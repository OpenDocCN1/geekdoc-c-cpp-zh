```
new WriteLine { Text = "The workflow has finished",
new Assign<string>
{
    To = new Argument<string>(ctx) => Result.Get(ctx),
    Value = new InArgument<string>(ctx) => temp.Get(ctx)
}
};

```

Code file [Program.cs] available for download at Wrox.com

When you run this application, you see that it produces similar output to HelloWorkflow. When you take a look at the Main method, you can see that here the Invoke method instantiates an internal workflow class named HelloWorkflow. Input arguments are passed, while output arguments are extracted exactly the same way as in the graphically designed workflow.

It may be surprising, but the workflow itself is an activity — that is HelloWorkflow derives from the Activity class:

```
internal class HelloWorkflow : Activity
{
    // ...
}

```

The activities is assumed to execute are defined in a declarative fashion. Look at the constructor of the class:

```
public HelloWorkflow()
{
    var temp = new Variable<string>("temp");
    Implementation = () =>
        new Sequence
        // ...
}

```

The Implementation property is a type of Func<Activity> and the lambda expression used here declares the Sequence activity with all nested activities. Because it is just a declaration, creating this lambda expression is a cheap operation. When the workflow is about to be executed, the method represented by the lambda behind Implementation is called.

# Declaring Workflow Arguments

Workflow arguments are declared as simple read-write properties:

```
public InArgument<String> Message { get; set; }
outArgument<String> Result { get; set; }

```