# In the Spotlight:

Notice that the hierarchy chart does not show the steps that are taken inside a module. Because hierarchy charts do not reveal any details about how modules work, they do not replace flowcharts or pseudocode.

# Defining and Calling Modules

Professional Appliance Service, Inc. offers maintenance and repair services for house-appliances. The owner wants to give each of the company’s service technicians a small handheld computer that displays step-by-step instructions for many of the repairs they perform. To see how this might work, the owner has asked you to develop a program that displays the following instructions for disassembling an ACME dryer:

+   1. Unplug the dryer and move it away from the wall.
2. Remove the six screws from the back of the dryer.
3. Remove the dryer's back panel.
4. Pull the top of the dryer straight up.

During your interview with the owner, you determine that the program should display the steps one at a time. You decide that after each step is displayed, the user will be asked to press a key to see the next step. Here is the algorithm for the program:

+   1. Display a starting message, explaining what the program does.
2. Ask the user to press a key to see Step 1.
3. Display the instructions for Step 1.
4. Ask the user to press a key to see the next step.
5. Display the instructions for Step 2.
6. Ask the user to press a key to see the next step.
7. Display the instructions for Step 3.
8. Ask the user to press a key to see the next step.
9. Display the instructions for Step 4.

This algorithm lists the top level of tasks that the program needs to perform, and becomes the basis of the program’s main module. Figure 3-8 shows the program’s structure in a hierarchy chart.

Figure 3-8 Hierarchy chart for the program

![](bbox=[0.125, 0.792, 0.875, 0.995])