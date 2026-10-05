# 10.5 The Order in “catch”

With the single catch in main() from Listing 10.2, I caught all possible exceptions in my program. Both std::invalid_argument and ios_base::failure can be converted to the specified std::exception. However, you can also use two separate handlers:

```
int main() {
  try {
    // Code as before
    return 0; // if everything is okay, return ok as well
  catch(std::invalid_argument &exc) { // first handler
    cerr << "Invalid argument: " << exc.what() << "\n"
  } catch(std::base::failure &exc) { // second handler
    cerr << "File error: " << exc.what() << "\n"
  } catch(std::exception &exc) { // third, very general handler
    cerr << "An error occurred: " << exc.what() << "\n"
  } catch (...) { // fourth and last handler for the rest
    cerr << "A strange error occurred\n";
  }
  return 1; // you only get here after a catch: report error
}
```

If an invalid_argument exception occurs between the catch blocks, the catch handlers are tried in order—and the first one, invalid_argument matches. The handler is executed and then the entire handler block is exited; the next line is therefore return 1. Unlike with switch, there is no fall-through to the next handler here.

If the code throws an ios_base::failure exception, then invalid_argument does not match, and the second handler is tried. It matches and is executed. Even after this handler, the program continues after the last catch.