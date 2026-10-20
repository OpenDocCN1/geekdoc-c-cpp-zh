```
23    try // throw an exception and immediately catch it
24    {
25        System.out.println( "Method throwException" );
26        throw new Exception(); // generate exception
27    } // end try
28    catch ( Exception exception ) // catch exception thrown in try
29    {
30        System.err.println(
31            "Exception handled in method throwException" );
32        throw exception; // rethrow for further processing
33
34        // code here would not be reached; would cause compilation errors
35
36    } // end catch
37    finally // executes regardless of what occurs in try...catch
38    {
39        System.err.println( "Finally executed in throwException" );
40    } // end finally
41
42        // code here would not be reached; would cause compilation errors
43
44    } // end method throwException
45
46    // demonstrate finally when no exception occurs
47    public static void doesNotThrowException()
48    {
49        try // try block does not throw an exception
50        {
51            System.out.println( "Method doesNotThrowException" );
52        } // end try
53        catch ( Exception exception ) // does not execute
54        {
55            System.err.println( exception );
56        } // end catch
57        finally // executes regardless of what occurs in try...catch
58        {
59            System.err.println(
60                "Finally executed in doesNotThrowException" );
61        } // end finally
62
63        System.out.println( "End of method doesNotThrowException" );
64    } // end method doesNotThrowException
65    } // end class UsingExceptions
```

Method throwException
Exception handled in method throwException
Finally executed in throwException
Exception handled in main
Method doesNotThrowException
Finally executed in doesNotThrowException
End of method doesNotThrowException

Fig. 11.4 | try...catch...finally exception-handling mechanism. (Part 2 of 2.)