```
```cpp
139    return tempPtr; // return the newly created object
140 } // end function createTransaction
```
```

# **Fig. 26.15 |** ATM class member-function definitions (Part 4 of 4)

Line 10 declares an enum named MenuOption that contains constants corresponding to the four options in the ATM’s main menu (i.e., balance inquiry, withdrawal, deposit and exit). Note that setting BALANCE_INQUIRY to 1 causes the subsequent enumeration constants to be assigned the values 2, 3 and 4, as enumeration constant values increment by 1.

Lines 13–18 define class ATM’s constructor, which initializes the class’s data members. When an ATM object is first created, no user is authenticated, so line 14 uses a member initializer to set userAuthenticated to false. Likewise, line 15 initializes currentAccountNumber to 0 because there is no current user yet.

# *ATM Member Function run*

ATM member function run (lines 21–38) uses an infinite loop (lines 24–37) to repeatedly welcome a user, attempt to authenticate the user and, if authentication succeeds, allow the user to perform transactions. After an authenticated user performs the desired transactions and chooses to exit, the ATM resets itself, displays a goodbye message to the user and re-starts the process. We use an infinite loop here to simulate the fact that an ATM appears to run continuously until the bank turns it off (an action beyond the user’s control). An ATM user has the option to exit the system, but does not have the ability to turn off the ATM completely.

# *Authenticating a User*

Inside member function run’s infinite loop, lines 27–31 cause the ATM to repeatedly welcome and attempt to authenticate the user as long as the user has not been authenticated (i.e., !userAuthenticated is true). Line 29 invokes member function displayMessageLine of the ATM’s screen to display a welcome message. Like Screen member function displayMessageLine designed in the case study, member function displayMessageLine (declared in line 13 of Fig. 26.16 and defined in lines 20–23 of Fig. 26.17) displays a message to the user, but this member function also outputs a newline after displaying the message. We’ve added this member function during implementation to give class Screen’s clients more control over the placement of displayed messages. Line 30 of Fig. 26.15 invokes class ATM’s private utility function authenticateUser (lines 41–60) to attempt to authenticate the user.

We refer to the requirements specification to determine the steps necessary to authenticate the user before allowing transactions to occur. Line 43 of member function authenticateUser invokes member function displayMessage of the ATM’s screen to prompt the user to enter an account number. Line 44 invokes member function getInput of the ATM’s keypad to obtain the user’s input, then stores the integer value entered by the user in a local variable accountNumber. Member function authenticateUser next prompts the user to enter a PIN (line 45), and stores the PIN input by the user in a local variable pin (line 46). Next, lines 49–50 attempt to authenticate the user by passing the accountNumber and pin entered by the user to the bankDatabase’s authenticateUser member function. Class ATM sets its userAuthenticated data member to the bool value returned by this function—userAuthenticated becomes true if authentication succeeds (i.e., accountNumber and pin match those of an existing Account in bankDatabase) and remains false otherwise.