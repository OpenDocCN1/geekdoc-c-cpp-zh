# Answers to Self-Test Exercises

<< "with a remainder of " << (number1%number2)
<< "\n";

```
return 0;
}
```

+   8. 52.0

+   b. 9/5 has int value 1. Since the numerator and denominator are both, integer division is done; the fractional part is discarded. The programmer probably wanted floating-point division, which does not discard the part after the decimal.

+   c. f = (9.0/5) * c + 32.0;

```
f = 1.8 * c + 32.0;
```

+   9. cout << "The answer to the question of\n"
<< "Life, the Universe, and Everything is 42.\n";

+   10. cout << "Enter a whole number and Return: \"
cin >>number;"

+   11. cout.setf(ios::fixed);
out.set(ios::showpoint);
cout.precision(3);

+   12. #include <iostream>
using namespace std;

```
int main() {
    cout << "Hello world!\n"
    return 0;
}
```

Other answers are correct. For example, the letters could be in double quotes instead of single quotes. Another possible answer is the following:
cout << "\A\nBC";

+   14. cin reads up to the next whitespace, so the first and last name cannot be read into a string if there is a space between the first name and last name. The easiest solution is to read the first and last name into two variables:

```
string first, last;
int age;
out << "Enter your first and last name." << endl;
cin >> first >> last;
out << "Enter your age." << endl;
cin >> age;
out << "You are " << age << " years old, " << first << " " << last << "" << endl;
```

+   15. The + operator concatenates two strings. The result is s3 = "53". If s1 and s2 are numeric types, then the values would be added.