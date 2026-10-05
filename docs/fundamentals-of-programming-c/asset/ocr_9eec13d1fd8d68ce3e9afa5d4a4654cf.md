# 11.1. VECTORS

```
int main() {
  const int SIZE = 3;
  vector<int> a(5, 5);
  // Print the contents of the vector
  cout << "a contains";
  for (int i = 0; i < SIZE; i++)
    cout << a[i] << " ";n  cout << endl;
  // Change all the 5s in vector to 8s Bug: <= should be <
  for (int i = 0; i < SIZE; i++)
    a[i] = 8;
  // Reprint the contents of the vector
  cout << "a contains";
  for (int i = 0; i < SIZE; i++)
    cout << a[i];
  cout << endl;
}
```

11.4 vectoroutofbounds contains a logic error: accessing to elements outside the bounds of a vector produces what is known as undefined behavior. The C++ language standard uses this term to indicate a program's behavior is not specified, and writers are free to do whatever they want. Running programs that venture into undefined behavior will crash, but they may continue executing without indication of a problem and behave correctly most. In other words, the actual behavior is system and compiler dependent. Consider code that represents undefined behavior to be a logic error, its action is incorrect. Simply saying, the program's behavior is unpredictable.

In most cases, an out-of-bounds access simply accesses memory outside the vector. This includes memory that does not belong to the executing program, modern operating systems will terminate the program and produce an error message. Under Visual C++ when the program is built as a debug version (the default) it prints the contents of the vector the first time but crashes before it can print it a second time. Microsoft Windows then displays the dialog box in Figure 11.4. The program running under Linux or OS X may simply print fault in the console:

> Segmentation fault

If you are using a vector, and it terminates with such a message, you should check your source code carefully for places where out-of-bounds vector accesses are possible.

The following code fragment shows some proper and improper vector accesses:

```
vector<int> numbers(10); // Declare the vector
numbers[0] = 5; // Put value 5 first
numbers[9] = 2; // Put value 2 last
numbers[-1] = 5; // Out of bounds; first valid index is 0
numbers[10] = 5; // Out of bounds; last valid index is 9
numbers[1.3] = 5; // Compiler warning, 1.3 is not an int
```

In a vector traversal with a for loop such as