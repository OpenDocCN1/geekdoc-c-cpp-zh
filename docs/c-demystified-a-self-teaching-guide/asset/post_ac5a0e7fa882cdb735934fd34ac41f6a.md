
![](img/59a3417a6d5906fae6d8000d4c2cff76_103_0.png)

**Figure 5-6:** Flowchart depiction of the grade determination program

Let’s now analyze the program.

The **switch** keyword evaluates an integer expression, *grade*. While grade is a variable, every case has a corresponding integer value.

Earlier in this chapter, we discussed flowchart symbols prescribed by the American National Standard Institute (ANSI), and mentioned that ANSI prescribes other standards that we will use in this chapter. One of other standards is the ANSI character set, which includes 256 characters, each having an integer value between 0 and 255. These values are also referred as ASCII values, which values from 0 to 127 of the ANSI character set are the same as the ASCII (American Standard Code for Information Interchange) character set.

Table 5-4 lists the ANSI/ASCII values for commonly used characters. Note that digits also be characters, and that the ANSI/ASCII value of an uppercase character is different than the value of the corresponding lowercase character.

**Table 5-4:** Selected ANSI/ASCII Values

| Character | Value |
| :--- | :--- |
| 0 | 48 |
| 9 | 57 |
| A | 65 |
| Z | 90 |
| a | 97 |
| z | 122 |

Each **case** keyword is followed by an integer expression that must be constant, that is, it cannot change in value during the life of the program. Therefore, a variable cannot follow a case keyword. In this program, the constant is a character literal, as A, B, and so forth-on. Each character's value is an ANSI value, and the integer expression is followed by a colon.

### Caution

A common mistake is to follow the integer expression not with a colon but a semicolon, which is typically used to terminate statements. This will cause a compiler error.

The default keyword serves the same purpose as an else part in an if /else /else statement, and is therefore not followed by an integer expression.

The integer expression following the switch keyword is evaluated and compared with the integer constant following each keyword, from top to bottom. If there is a match—that is, if two integers are equal—then the statements belonging to that case are executed. Otherwise, they are not. Thus, the statements belonging to a case are conditional, just as statements in if, else, or else part. However, unlike an if /else statement, multiple conditional statements belonging to a case do not need to be enclosed in curly braces.

### Differences Between switch and if /else /else Statements

While a switch statement is similar to an if /else /else statement, there are important differences.

One difference is that in an if /else /else statement, the comparison following the if part may be independent of the comparison following the else part. While a bit silly, is illustrative of this concept:

```cpp
if (apples == oranges)
  do;
else if (sales >= 5000)
  do;
```

By contrast, in a switch statement, the constant integer expression following a case keyword must be compared with the value following the switch keyword, and nothing else. The next chapter on logical operators discusses other differences between switch and if /else /else statements. However, two differences can be discussed now. One is commonly known as "falling through". Other concerns ranges of numbers.

### Falling Through

In an if /else /else statement, each part is separate from the others. By contrast, a switch statement (once a match is found) unless a break statement is executed, "falls through" to the next case. For example, if you removed the break statement from the switch, you could have the following:

```text
Enter grade:
Your average must be between 90-100
Your average must be between 80-89
Your average must be between 70-79
Your average must be 60
```

This "falling through" behavior is not necessarily desired. The following program shows this:

```cpp
#include <iostream>
using namespace std;

int main() {
    char grade;
    cout << "Enter grade: ";
    cin >> grade;
    switch (grade) {
        case 'A':
            cout << "Your average is between 90-100" << endl;
        case 'B':
            cout << "Your average is between 80-89" << endl;
        case 'C':
            cout << "Your average is between 70-79" << endl;
        case 'D':
            cout << "Your average is 60" << endl;
        default:
            cout << "Your average is below" << endl;
    }
    return 0;
}
```

```cpp
#include <iostream>
using namespace std;

int main() {
    char grade;
    cout << "Enter grade: ";
    cin >> grade;
    switch (grade) {
        case 'A':
            cout << "Your average is between 90-100" << endl;
            break;
        case 'B':
            cout << "Your average is between 80-89" << endl;
            break;
        case 'C':
            cout << "Your average is between 70-79" << endl;
            break;
        case 'D':
            cout << "Your average is 60" << endl;
            break;
        default:
            cout << "Your average is below" << endl;
    }
    return 0;
}
```

### Ranges of Numbers

Another difference between switch and if /else /else statements is handling ranges of numbers. In an if /else /else statement, each part is separate from the others:

```cpp
if (testScore >= 90)
  cout << "90-100" << endl;
else if (testScore >= 80)
  cout << "80-89" << endl;
```

By contrast, in a switch statement, the case keywords must be followed by constant integers. However, you can use multiple cases to represent a range:

```cpp
switch (testScore) {
    case 100:
    case 99:
    case 98:
    case 97:
    case 96:
    case 95:
    case 94:
    case 93:
    case 92:
    case 91:
    case 90:
        cout << "90-100" << endl;
        break;
    case 89:
    case 88:
    case 87:
    case 86:
    case 85:
    case 84:
    case 83:
    case 82:
    case 81:
    case 80:
        cout << "80-89" << endl;
        break;
}
```

![](img/59a3417a6d5906fae6d8000d4c2cff76_105_0.png)
