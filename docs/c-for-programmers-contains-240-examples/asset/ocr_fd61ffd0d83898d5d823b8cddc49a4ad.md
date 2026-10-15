ating and executing financial transactions. To authenticate a user and perform transactions, the ATM must interact with the bank’s account information database. [Note: A database is an organized collection of data stored on a computer.] For each bank account, the database stores an account number, a PIN and a balance indicating the amount of money in the account. [Note: For simplicity, we assume that the bank plans to build only one ATM, so we do not need to worry about multiple ATMs accessing this database at the same time. Furthermore, we assume that the bank does not make any changes to the information in the database while a user is accessing the ATM. Also, any business system like an ATM faces reasonably complicated security issues that go well beyond the scope of a first- or second-semester computer science course. We make the simplifying assumption, however, that the bank trusts the ATM to access and manipulate the information in the database without significant security measures.]

Upon first approaching the ATM, the user should experience the following sequence of events (shown in Fig. 2.11):

+   1. The screen displays a welcome message and prompts the user to enter an account number.
+   2. The user enters a five-digit account number, using the keypad.
+   3. The screen prompts the user to enter the PIN (personal identification number) associated with the specified account number.
+   4. The user enters a five-digit PIN, using the keypad.
+   5. If the user enters a valid account number and the correct PIN for that account, the screen displays the main menu (Fig. 2.12). If the user enters an invalid account number or an incorrect PIN, the screen displays an appropriate message, then the ATM returns to Step 1 to restart the authentication process.

![](bbox=[0.16, 0.62, 0.8, 0.9])

Fig. 2.12 | ATM main menu.