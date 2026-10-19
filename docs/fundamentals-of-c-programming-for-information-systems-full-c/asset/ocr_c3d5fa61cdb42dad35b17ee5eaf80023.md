The **process** specifies not only **what** the program should do (e.g., compute total cost) but also **how** it should be done (e.g., how to compute total cost), as follows:

Process: (What?)      Look up unit price, look up sales tax rate,
compute subtotal, sales tax and total cost
(How?)      subtotal:  unit price * order quantity
sales tax:  subtotal * sales tax rate
total cost: subtotal + sales tax

Specifying the process also would include identifying the sources of data, like the product file to get the unit price and sales tax file to get the sales tax rate.

The **input** specifies the data items that are needed to carry out the process to produce the output. The input for this order-processing system would be

Input:      item number, order quantity

Note that unit price and sales tax rate are not included in the input because the program looks them up. A real-world system would be a lot more complex. Typically, the process would include additional subtasks like handling orders when inventory is insufficient, and output may include various reports. In such systems, graphical methods like **Data Flow Diagrams** and **UML diagrams** are used to represent the processes and the data accessed by them.

# 2. Design and develop the graphical user interface (GUI)

After identifying the input, process and output of a program, you design and create the user interface—that is, how the user would interact with the program, and how the program would communicate with the user. This is the fun part where you bring in your creativity.

Typically, you use forms to interact with the program. As you will learn in the next section, forms have various types of objects, called **controls**, such as Button, TextBox and Label. In this step, you identify the type of controls to be used, specify their names and captions as appropriate, and design the layout. Figure 1-3 shows an example of the GUI for a simplified order-processing system where the user doesn’t provide the unit price and sales tax rate.

Figure 1-3: GUI for an order-processing system

![](bbox=[0.13, 0.71, 0.79, 0.89])