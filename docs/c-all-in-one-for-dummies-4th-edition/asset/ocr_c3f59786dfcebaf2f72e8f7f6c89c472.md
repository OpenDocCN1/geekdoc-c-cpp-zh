```
```cpp
numAsString += ch;
}

// Get the next character from the user.
ch = getch();
}

return numAsString;
}

string EnterPassword() {
    // Holds the password string.
    string numAsString = "";
    // Obtains a single character from the user.
    char ch = getch();

    // Keep requesting characters until the user presses
    // Enter.
    while (ch != '\r') { // \r is the enter key
        // Display an asterisk instead of the input character.
        cout << '*';
        // Add the character to the password string.
        numAsString += ch;
        // Get the next character from the user.
        ch = getch();
    }

    return numAsString;
}

int main() {
    // Just a basic name-entering
    string name;
    cout << "What is your name? ";
    cin >> name;
    cout << "Hello " << name << endl;

    // Now you are asked to enter a number,
    // but the computer allows you to enter anything!
    int x;
    cout << endl;
    cout << "Enter a number, any number! ";
```
```

*(continued)*