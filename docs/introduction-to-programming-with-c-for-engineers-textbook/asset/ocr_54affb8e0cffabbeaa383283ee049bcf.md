| Caption | Meaning | Examples |
|---|---|---|
|  |  | To define a variadic template function, we need two versions of that function: the startup version defined on lines [62–67], and the version with the template parameter pack Args, defined on lines [70–77]. This structure follows the recursive call type that happens on line [76]. Hence, at the end of the recursion, the startup version ends the call.

```cpp
void multi_print_helper_test( void )
{
    // Make a log file
    ofstream log_file("log_file.txt");

    // A helper variable lambda that joins multi_print_helper with the log file
    auto diagnostic_print = [& log = log_file]( auto... params ) -> ostream &
    {
        // Each output separate with "," then add end-of-line
        return multi_print_helper( log, ", ", params ... ) << endl;
    };

    int x( 1 ); double y( 2.0 ); string z ( "error" );

    // Output objects of arbitrary type to the log file
    diagnostic_print( x, y, z );

    diagnostic_print( x, y, z, "text", x == y, 5.0 );
}
```

The `multi_print_helper_test` function shows a use context for the variadic template `multi_print_helper` function. However, since we should never wish to redirect output to the diagnostic file created on line [81], a helper lambda with variadic parameters is introduced on lines [84–87]. The only action it performs, on line [86], is to call `multi_print_helper` with properly organized parameters. Finally, the previous lambda is called on lines [93] and [95], each time with a different number of input parameters of arbitrary types. Finally, the content of the `log_file.txt` looks like the following:

```text
1 2 three
2 three Text: 0.5
``` |