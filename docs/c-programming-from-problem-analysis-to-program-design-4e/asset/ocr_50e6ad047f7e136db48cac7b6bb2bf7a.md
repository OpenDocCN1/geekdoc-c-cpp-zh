![](bbox=[0.202, 0.12, 0.71, 0.591])

The manager of the Diner by the Valley campus deli plans to have a computer available for students to place their orders when they enter the campus center. They have a limited menu selection available that includes sandwiches and drinks. The manager wants the computer screen to allow the students to select from a list of available sandwich and drink options. A large board is located on the wall at the location where the computer will reside. It shows the menu of items available and lists the price of each item.

A user-friendly interface is needed. Water is available for each order at no charge, but it must be ordered. In addition to white bread, they have whole wheat and rye bread. No charge is included for different bread types; however, they do consider that selection a special request. The interface should enable special requests such as bread types to be selected. Students should be able to enter other special requests such as “Hold the onion” or “Hold the mayo.”

Design a GUI that accepts as input food and drink selections. The manager would like to have options for showing the total cost of the order, displaying the current order selections, or allowing students to change their minds about each of the selections.

**FIGURE 10-24** Problem specification for DinerGUI example

# ANALYZE THE PROBLEM

You should review the problem specification in Figure 10-24 and make sure you understand the problem definition. Several values will be selected from GUI controls to represent the entree and drink selections, as well as preferences for water and special requests. The business logic is separated from the user interface using two classes. The data members for the Order class are shown in Table 10-6.