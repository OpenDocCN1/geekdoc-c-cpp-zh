# # Programming with the Streams Library

The libraries you use to work with streams are divided into various groups, each of which requires its own header. The libraries divide input and output into separate classes, as shown in Figure 1-1. In addition, the kind of input and output determines which header you use. The libraries also support specific commands that include `cin` and `cout` — the commands you have used for so many purposes so far.

![](bbox=[0.248, 0.275, 0.767, 0.649])

**FIGURE 1-1:**  
Working with streams requires use of the appropriate headers and commands.

Now that you have a basic overview of how these various headers and commands work with the streams library to provide stream output, it’s time to get the details. The following sections help you understand how to use code to create streams of data that could go to a file, Internet connection, or some other location, such as a smart speaker.

# ## Getting the right header file

The streams library includes several classes that make your life much easier. It also has several classes that can make your life more complicated, mainly