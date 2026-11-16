# # PRESENTATION PATTERNS

There are several common patterns for the Presentation layer, and each one has a number of variations, but they all have the same basic goal: to separate the widgets the user sees from the logic that maintains the data those widgets displays or responds to interactions the user has with the widgets. This is often described as separating state and behavior from presentation.

The presentation logic is called different things in different patterns. It represents the state and behavior of the interface.

The presentation logic provides data to the presentation widgets, and receives notification of anything the user does like change some data or click a button.

The presentation logic interacts with the model to retrieve information and issue commands.

![](bbox=[0.23, 0.37, 0.86, 0.65])

The view is the actual interface with which the user interacts.

Some patterns allow the View to know about the Model; some don't.

The model is responsible for actually processing the data.

The user don't care about any of this. They just have a job to do.

![](bbox=[0.1, 0.75, 0.26, 0.87])

## ON YOUR OWN

When you separate the logic behind an interface from the interface itself, it becomes much easier to do a couple of things. Do you know what they are? (Hint: both words begin with “re”.)