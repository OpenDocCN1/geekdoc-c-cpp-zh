# Unwinding the Stack

Suppose a try block doesn't contain a direct call to a function that throws an exception but that it calls a function that calls a function that throws an exception. Execution jumps to the function in which the exception is thrown to the function that try block and handlers. Doing so involves unwinding the stack, which we'll discuss now.

First, let's look at how C++ normally handles function calls and returns. C++ typically handles function calls by placing information on a stack (see Chapter 9,"Memory Models and Namespaces"). In particular, the program places the address of a calling function instruction (a return address) on the stack. When the called function completes, the program uses that address to determine where to continue with program execution. Also the function call places any arguments on the stack, where they are treated as automatic variables. If the called function creates any new automatic variables, they, too, are added to the stack. If a called function calls another function, its information is added to the stack, and so on. When a function terminates, program execution passes to the address stored when the function was, and the top of the stack is freed. This function normally returns to the function that called it, with each function liberating its automatic variables as it terminates. If an automatic variable is a class object, then the destructor if any, is called.

Suppose a function terminates via a thrown exception instead of a return call. Again, the program frees memory from the stack. But instead of stopping at the first return address on the stack, the program continues freeing the stack until it reaches a return address that resides in a try block (see Figure 15.3). Control passes to the exception handlers at the end of the block rather than to the first statement following the function call. This process is called unwinding the stack. One important feature of the throw mechanism is that, just as with function returns, the class destructors are called for any automatic class objects on the stack by that function, whereas the throw statement processes objects put on the stack by the entire sequence of function calls between the try block and the throw. Without the unwinding-stack feature, a throw would leave destructors undeared for automatic class objects placed on the stack by intermediate function calls.

Listing 15.12 provides an example of unwinding the stack. In it, main() calls mean(), which turn calls hmean() and gmean().The .mean() function, for the sake of anything better to do, calculates the mean of the arithmetic, harmonic, and geometric means. Both main() and mean() create objects of the demo type (a babbling class that announces when its constructor and destructor are used) so that you can see what happens to those objects when exceptions are thrown. The try block in main() catches both bad_hmean and bad_gmean exceptions, the try block in means catches just the bad_hmean exception. This catch block has the following code:

```
catch (bad_hmean & bg) // start of catch block
{
  bg.mesg();
  std::cout << "Caught in mean()\n";
  throw;              // rethrows the exception
}
```