object account1’s credit method and supplies depositAmount as the method’s argument. When the method is called, the argument’s value is assigned to parameter amount (line 19 of Fig. 3.13) of method credit (lines 19–22 of Fig. 3.13); then method credit adds that value to the balance (line 21 of Fig. 3.13). Lines 30–33 (Fig. 3.14) output the balances of both Accounts again to show that only account1’s balance changed.

Line 35 prompts the user to enter a deposit amount for account2. Line 36 obtains the input from the user by calling Scanner object input’s nextDouble method. Lines 37–38 display the deposit amount. Line 39 calls object account2’s credit method and supplies depositAmount as the method’s argument; then method credit adds that value to the balance. Finally, lines 42–45 output the balances of both Accounts again to show that only account2’s balance changed.

# UML Class Diagram for Class Account

The UML class diagram in Fig. 3.15 models class Account of Fig. 3.13. The diagram models the private attribute balance with UML type Double to correspond to the class’s instance variable balance of Java type double. The diagram models class Account’s constructor with a parameter initialBalance of UML type Double in the third compartment of the class. The class’s two public methods are modeled as operations in the third compartment as well. The diagram models operation credit with an amount parameter of UML type Double (because the corresponding method has an amount parameter of Java type double), and operation getBalance with a return type of Double (because the corresponding Java method returns a double value).

![](bbox=[0.35, 0.55, 0.65, 0.68])

Fig. 3.15 | UML class diagram indicating that class Account has a private balance attribute of UML type Double, a constructor (with a parameter of UML type Double) and two public operations—credit (with an amount parameter of UML type Double) and getBalance (returns UML type Double).

# 3.8 (Optional) GUI and Graphics Case Study: Using Dialog Boxes

This optional case study is designed for those who want to begin learning Java’s powerful capabilities for creating graphical user interfaces (GUIs) and graphics early in the book, before the main discussions of these topics in Chapter 14, GUI Components: Part 1, Chapter 15, Graphics and Java 2D, and Chapter 25, GUI Components: Part 2.

The GUI and Graphics Case Study appears in 10 brief sections (see Fig. 3.16). Each section introduces new concepts and provides examples with screen captures that show sample interactions and results. In the first few sections, you’ll create your first graphical applications. In subsequent sections, you’ll use object-oriented programming concepts to