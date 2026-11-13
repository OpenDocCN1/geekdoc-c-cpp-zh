
## CONVERTING INPUT TO UPPERCASE LETTERS

Even small test programs should have some flexibility regarding user input. For example, the program should accept either upper- or lowercase letters for each menu choice. We accomplish this by reading the user's input and then, if necessary, converting a lowercase letter to the corresponding uppercase letter. The conversion is carried out by a function toupper with this specification:

```
char toupper(char c);
// Postcondition: If c is a lowercase letter, then the return value is the
//   uppercase equivalent of c. Otherwise the return value is just c itself.
```

The toupper function is part of the <cctype> facility. In our main program, we use toupper to convert the result of the get_user_command function, as shown here:

```
choice = toupper(get_user_command ( ));
```

## FIGURE 3.10 Interactive Test Program for the Sequence Class

### A Program

```
// FILE: sequence_test.cxx
// An interactive test program for the new sequence class
#include <cctype> // Provides toupper
#include <iostream> // Provides cout and cin
#include <cstdlib> // Provides EXIT_SUCCESS
#include "sequence.h" // With value_type defined as double
using namespace std;
using namespace main_savitch_3;

// PROTOTYPES for functions used by this test program:
void print_menu( );
// Postcondition: A menu of choices for this program has been written to cout.
char get_user_command( );
// Postcondition: The user has been prompted to enter a one-character command.
//   The next character has been read (skipping blanks and newline characters),
//   and this character has been returned.
void show_sequence(sequence display);
// Postcondition: The items on display have been printed to cout (one per line).
double get_number( );
// Postcondition: The user has been prompted to enter a real number. The
//   number has been read, echoed to the screen, and returned by the function.
int main()
{
    sequence test; // A sequence that we'll perform tests on
    char choice; // A command character entered by the user
    cout << "I have initialized an empty sequence of real numbers." << endl;
    do
    {
        print_menu();
        choice = toupper(get_user_command());
        switch (choice)
        {
            case '!': test.start();
                break;
            case '+': test.advance();
                break;
            case '?': if (test.is_item())
                cout << "There is an item." << endl;
            else
                cout << "There is no current item." << endl;
            case 'C': if (test.is_item())
                cout << "Current item is: " << test.current() << endl;
            else
                cout << "There is no current item." << endl;
            case 'P': show_sequence(test);
            case 'S': cout << "Size is " << test.size() << '.' << endl;
                break;
            case 'I': test.insert(get_number());
                break;
            case 'A': test.attach(get_number());
                break;
            case 'R': test.remove_current();
                cout << "The current item has been removed." << endl;
                break;
            case 'Q': cout << "Ridicule is the best test of truth." << endl;
                break;
            default: cout << choice << " is invalid." << endl;
        }
    } while ((choice != 'Q'));
    return EXIT_SUCCESS;
}
```

## (FIGURE 3.10 continued)

```
void print_menu( )
// Library facilities used: iostream
{
    cout << endl; // Print blank line before the menu
    cout << "The following choices are available: " << endl;
    cout << " !   Activate the start( ) function" << endl;
    cout << " +   Activate the advance( ) function" << endl;
    cout << " ?   Print the result from the is_item( ) function" << endl;
    cout << " C   Print the result from the current( ) function" << endl;
    cout << " P   Print a copy of the entire sequence" << endl;
    cout << " S   Print the result from the size( ) function" << endl;
    cout << " I   Insert a new number with the insert(... ) function" << endl;
    cout << " A   Attach a new number with the attach(... ) function" << endl;
    cout << " R   Activate the remove_current( ) function" << endl;
    cout << " Q   Quit this test program" << endl;
}
```

```
char get_user_command( )
// Library facilities used: iostream
{
    char command;
    cout << "Enter choice: ";
    cin >> command; // Input of characters skips blanks and newline character
    return command;
}
```

```
void show_sequence(sequence display)
// Library facilities used: iostream
{
    for (display.start( ); display.is_item( ); display.advance( ))
        cout << display.current( ) << endl;
}
```

```
double get_number( )
// Library facilities used: iostream
{
    double result;
    cout << "Please enter a real number for the sequence: ";
    cin >> result;
    cout << result << " has been read." << endl;
    return result;
}
```

## FIGURE 3.11 Part of a Sample Dialogue from the Program of Figure 3.10

### A Sample Dialogue

I have initialized an empty sequence of real numbers.

The following choices are available:
! Activate the start( ) function
+ Activate the advance( ) function
? Print the result from the is_item( ) function
C Print the result from the current( ) function
P Print a copy of the entire sequence
S Print the result from the size( ) function
I Insert a new number with the insert(...) function
A Attach a new number with the attach(...) function
R Activate the remove_current( ) function
Q Quit this test program
Enter choice: A
Please enter a real number for the sequence: 3.14
3.14 has been read.

The following choices are available:
! Activate the start( ) function
+ Activate the advance( ) function
? Print the result from the is_item( ) function
C Print the result from the current( ) function
P Print a copy of the entire sequence
S Print the result from the size( ) function
I Insert a new number with the insert(...) function
A Attach a new number with the attach(...) function
R Activate the remove_current( ) function
Q Quit this test program
Enter choice: S
Size is 1.

The dialogue continues until the user types Q to stop the program.

## THE SWITCH STATEMENT

After the user's choice is read, the main program takes an action. The action depends on the single character that the user typed from the menu. An effective statement to select among many possible actions is the switch statement, with the general form:

```
switch (<Control value>)
{
    <Body of the switch statement>
}
```

When the switch statement is reached, the control value is evaluated. The program then looks through the body of the switch statement for a matching case label. For example, if the control value is the character 'A', then the program looks for a case label of the form case 'A':. If a matching case label is found, then the program goes to that label and begins executing statements. Statements are executed one after another—but if a break statement (of the form break;) occurs, then the program skips to the end of the body of the switch statement.

If the control value has no matching case label, then the program will look for a default label of the form default:. This label handles any control values that don't have their own case label.

If there is no matching case label and no default label, then the whole body of the switch statement is skipped.

For an interactive test program, the switch statement has one case label for each of the menu choices. For example, one of the menu choices is the character 'A', which allows the user to attach a new number to the sequence. In the switch statement, the 'A' command is handled as shown here:

```
switch (choice)
{
    ...
    case 'A': test.attach(get_number());
        break;
    ...
}
```

## Self-Test Exercises for Section 3.3

- 25. Name the library facilities that provide toupper, EXIT_SUCCESS, cout, and cin.

- 26. What are values of toupper('a'), toupper('A'), and toupper('+')?

- 27. What situation calls for a switch statement?

- 28. The show_sequence function on page 136 uses a value parameter rather than a reference parameter. Why?
