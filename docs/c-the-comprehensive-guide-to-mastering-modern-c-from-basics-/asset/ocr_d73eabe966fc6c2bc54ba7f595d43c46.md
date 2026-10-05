+   - With if(count < 0), I use the special return value of the function to react to the error.
- With if(result) in main(), I check the forwarded result.
Each case is handled differently:
- countWords returns a count (always zero or greater), so in countWords the return -1; with the special value of -1 indicates an error to the caller.
- The return value is checked in process if(count < 0), possibly specially handled, and finally passed outward at return result;
- The test in process if(args.size() == 0) can directly lead to a negative return via return false;
- And if an error occurs somewhere, it ultimately reaches bool result = process(); and is even passed to the callers of the program at return 1; from main().

If you react to errors in this way, you pass the error state through function calls using bool or int codes or—in extreme cases—separate error objects.
I want to quickly explain the argument {argv+1, argc} of process: The function receives a const vector<string>& as a parameter. However, the given argument is an initializer list consisting of const char*. The compiler can convert this without problems using the appropriate constructors of vector and string.

To show you how to use the program, here is how it reacts in different cases: