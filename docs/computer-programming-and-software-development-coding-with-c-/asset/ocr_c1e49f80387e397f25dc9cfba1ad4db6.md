will evolve ahead. We now have a dozen or so statements that execute in order from top to bottom without any variability. Our program flow is entirely sequential, and we can actually prove that using the Visual Studio debugging tools. I am going to assume you have at least basic familiarity with debugging in an IDE like Visual Studio. As a quick reminder, the debugger allows us to step through our code one line at a time as it executes. It also lets us inspect the state of variables and other context data along the way. We'll be using this tool throughout the book to walk through our program flow, so let's place a breakpoint to the left of line 10, which will tell the debugger where to initially pause so we can inspect our code.

![](bbox=[0.121, 0.399, 0.909, 0.438])

Next, let's run our app, and after this launches, we should land on the line of code where we set that point. This yellow highlighted bar indicates the next line of code that will be executed in our program flow.

![](bbox=[0.121, 0.618, 0.909, 0.66])

At the top of Visual Studio, we use our debugging controls to step through our app one line at a time. So as I click the step over arrow, we will slowly move from one line to the next in order.

![](bbox=[0.121, 0.816, 0.909, 0.925])