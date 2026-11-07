```
```cpp
int squareByValue(int number);  // prototype (for value pass)
void squareByReference(int& numberRef);  // prototype (for reference pass)

int main() {
    int x{2};  // value to square using squareByValue
    int z{4};  // value to square using squareByReference

    // demonstrate squareByValue
    cout << "x = " << x << " before squareByValue\n";
    cout << "Value returned by squareByValue: "
         << squareByValue(x) << '\n';
    cout << "x = " << x << " after squareByValue\n";

    // demonstrate squareByReference
    cout << "z = " << z << " before squareByReference\n";
    squareByReference(z);
    cout << "z = " << z << " after squareByReference\n";
}

// squareByValue multiplies number by itself, stores the
// result in number and returns the new value of number
int squareByValue(int number) {
    return number *= number;  // caller's argument not modified
}

// squareByReference multiplies numberRef by itself and stores the result
// in the variable to which numberRef refers in function main
void squareByReference(int& numberRef) {
    numberRef *= numberRef;  // caller's argument modified
}
```
```

```
```text
x = 2 before squareByValue
Value returned by squareByValue: 4
x = 2 after squareByValue

z = 4 before squareByReference
z = 16 after squareByReference
```
```

Fig. 5.8 | Passing arguments by value and by reference. (Part 2 of 2.)

# References as Aliases within a Function

References can also be used as aliases for other variables within a function (although they typically are used with functions, as shown in Fig. 5.8). For example, the code

```
```cpp
int count{1};  // declare integer variable count
int& cRef{count};  // create cRef as an alias for count
++cRef;  // increment count (using its alias cRef)
```
```

increments count by using its alias cRef. Reference variables must be initialized in their declarations and cannot be reassigned as aliases for other variables. In this sense, references are constant. All operations performed on the alias (i.e., the reference) are actually performed on the original variable. The alias is simply another name for the original variable. Unless it’s a reference to a constant (discussed below), a reference’s initializer must be an lvalue—something that can appear on the left side of an assignment, like a variable name.