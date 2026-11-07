![](bbox=[0.283, 0.084, 0.861, 0.264])

**Figure 6.1** A program made of several functions

When a task is more complicated, we divide the task into smaller tasks, in which each task is responsible for a part of the job. We see this approach in many other situations. For example, manufacturing a car is divided into several tasks. The body is made at one location, the engine is made somewhere else, another entity is responsible for making tires, and so on. When all of the parts are made and ready, the car is assembled.

The same approach can be applied to programming. We can divide a program into different sections, in which each section is responsible for a part of the task. Each section in this case is called a function in C++, although other terms with the same meaning, such as *method* or *procedure*, are also used. Figure 6.1 shows this approach.

In the figure, the responsibility of the program is still on the shoulder of the *main* function, but *main* calls other functions to do part of the job. The statements *input (...)*, *process (...)*, and *output (...)* are function calls that invoke the corresponding functions and let them do part of the job. When each function terminates, the control returns to the *main* function. The figure also shows that the *main* function is called by the C++ runner. When we run the program, the *main* function is invoked and does its task. In other words, we have used the concept of a function from the first program we wrote in the first chapter of this book. In this chapter, we develop the idea and learn how we can write more functions.

# ### 6.1.1 Benefits

You may wonder about the benefit of dividing a task into several small tasks when doing so involves writing more code because of the overhead involved in each function. Despite the extra work, there are benefits to task division, including the following.

# #### Easier to Write Simpler Task

Everyone knows that doing simple tasks is easier than doing difficult tasks. It is easier to concentrate on manufacturing tires for cars than manufacturing the whole car.

# #### Error Checking (Debugging)

One of the big headaches of programming is finding errors (called bugs). Error checking (or debugging) is much more simple when a program is divided into small functions. Each function can be debugged and then put together as one program.