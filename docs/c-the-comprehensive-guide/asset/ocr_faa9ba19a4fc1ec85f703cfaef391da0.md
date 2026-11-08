# ## 10.3 Minor Error Handling

Unlike in the first example, the processing now completely stops; for empty_file, you see no result. This is because the exception from open() is only caught in main()—and thus the for loop in process was also prematurely terminated.

If you want the same behavior—that is, continuing the processing with the next file—then you must not leave the for loop in passing. You need error handling within the loop.

```
```cpp
void process(const vector<string>& args) {
    if(args.size() == 0) {                  // expect parameters
        throw std::invalid_argument("Command line argument missing");
    } else {
        for(const string filename : args) {
            cout << filename << ": ";
            try {
                cout << countWords(filename) << "\n";
            } catch(std::exception &exc) {
                cout << "Error: " << exc.what() << "\n";
            }
        }
    }
}
```
```

**Listing 10.3** A “catch” can also be within a loop.

Now the error is caught and handled, and the for loop can continue normally with the next file.

The rest of the program remains the same. The throw std::invalid_argument is outside the try-catch block and reaches main() unchanged to be handled.

# ## 10.4 Throwing the Exception Again: “rethrow”

If you want both options—local error handling, but also error handling in main()—then you can use a throw without any argument within the catch block to rethrow the currently handled exception unchanged (hence the name rethrow).

```
```cpp
try {
    cout << countWords(filename) << "\n";
} catch(std::exception &exc) {
```
```