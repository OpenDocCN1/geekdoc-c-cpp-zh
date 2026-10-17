# # Figure 12.1
Abstraction generally allows you to view large sets of tasks in smaller sets.

![](bbox=[0.071, 0.106, 0.699, 0.401])

decomposition involves, among other things, asking a fairly rudimentary question: What is the order of the tasks to be performed? With the designation of an order of tasks comes the designation of dependencies. You know what you need for each task to be fulfilled. In Figure 12.1, for example, it makes little sense to check the spelling if no textual content exists.

Abstraction serves to eliminate dependencies. It accomplishes this feat by encapsulating code. Encapsulation ends up being an enormous asset in most industrial situations. Consider this: If you set up your programs so that the different functions you create are not tangled up with other functions, then you can more easily change one thing in isolation. This is one of the major benefits of encapsulation. Programmers can make isolated changes. The technical terms for this are loosely coupled and highly cohesive. In other words, the code in a function coheres: It makes sense when examined in isolation. A function is also loosely coupled with other functions, meaning that if you make changes to one function, you do not have to make changes in other functions.

# # Functional Abstraction in Programs

Figure 12.2 illustrates how you can use decomposition of the functionality to address the project depicted in Figure 12.1. The analysis involves four abstractions. Each abstraction relates to a task or set of tasks the program might perform as it provides the envisioned service. To access information involves in some way obtaining the information from some source. The source might be the program itself, a file containing text, or a database. Organizing information might involve sorting it or being able to select specific items from it. Processing user selections might involve taking input from the terminal. Displaying information might involve working with a DOS