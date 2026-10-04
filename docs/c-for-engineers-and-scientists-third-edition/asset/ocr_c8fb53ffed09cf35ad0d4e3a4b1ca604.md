# Problem Solving Using C++

programs (see Figure 2.1). Modular programs are easier to develop, correct, and modify than programs constructed in some other manner.

![](bbox=[0.248, 0.175, 0.752, 0.319])

**Figure 2.1** A well-designed program is built by using modules

Each module is designed and developed to perform a specific task and is actually a small subsum. A complete C++ program is constructed by combining as many modules as necessary to produce the desired result. The advantage of modular construction is that you can develop the program’s overall design before writing any modules. After finalizing requirements for each module, you can then program the modules and integrate them into the overall program as they become.
In C++, modules can be called functions. It helps to think of a **function** as a small machine that transforms the data it receives into a finished product. For example, Figure 2.2 illustrates a function that accepts two numbers as inputs and multiplies the two numbers to produce one output. The process of converting inputs to results is encapsulated and hidden in the function. In this regard, the function can be thought of as a single unit providing a special-purpose operation.

![](bbox=[0.296, 0.587, 0.703, 0.869])

**Figure 2.2** A multiplying function