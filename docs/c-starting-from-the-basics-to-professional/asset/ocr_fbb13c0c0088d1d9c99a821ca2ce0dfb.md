Exercise 16-4. Pick any number of Standard Library exception types from Figure 16-8 and write a program that causes each of those to be raised in turn (without actually throwing them yourself, of course). You should catch each of these exceptions and output the `what()` messages they contain, before moving on to triggering the next exception.

Exercise 16-5. Create a function called `readEvenNumber()` intended to read an even integer from the `std::cin` stream. At the start of some reading, read happens inside `readEvenNumber()`, resulting in a CurveBall exception. You can simply reuse code from Exercise 16-4 for this. Normally, however, the function verifies the user input and returns an even number if the user enters one correctly. If the input is not valid, however, the function throws one of the following exceptions:

+   - If any value is entered that is not a number, it throws a NotANumber exception.
+   - If the user enters a negative number, a NegativeNumber exception is thrown.
+   - If the user enters an odd number, the function throws an OddNumber exception.

You should derive these new exception types from `std::domain_error`, one of the standard exception types defined in the `<stdexcept>` module. Their constructors should compose a string containing at least the incorrectly entered value and then forward that string to the constructor of `std::domain_error`.

Hint: After attempting to read an integer number from `std::cin`, you can check whether parsing that integer succeeded by using `std::cin.fail()`. If that member function returns true, the user entered a string that is not a number. Notice that once the stream is in such a failure state, you cannot use the stream anymore until you call `std::cin.clear()`. Also, the nonnumeric value the user entered will still be inside the stream—it is not removed when failing to extract an integer. You could, for instance, extract it using the `std::getline()` function defined in a string. Putting this all together, your code might contain something like this:

```
if (std::cin.fail())
{
    std::cin.clear();    // Reset the failure state
    std::string line;    // Read the erroneous input and discard it
    std::getline(std::cin, line);
}
```

Once the `readEvenNumber()` helper is ready, use it to implement `askEvenNumber()`. This function prints user instructions to `std::cout` and then calls `readEvenNumber()` to handle the actual input and input verification. Once a number is read correctly, `askEvenNumber()` politely thanks the user for entering the number and the message should contain the number itself. For any `std::exception` that `readEvenNumber()` throws, `askEvenNumber()` should at least output a `what()` to `std::exception` that is not a domain error so it is to be rethrown, and `askEvenNumber()` has no idea how to handle these. If the exception is a `domain_error`, however, you should retry asking for an even number, unless the exception is a NotANumber. If a NotANumber occurs, askEvenNumber() stops asking for numbers and simply returns.