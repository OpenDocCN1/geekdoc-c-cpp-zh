# 27.4.1 Methods for Handling Stream Errors

To query the individual states, C++ offers you various methods:

+   - `bool good()`  
+     Returns true if everything is okay (`goodbit` is set).
+   - `bool eof()`  
+     Returns true if the file stream has ended (`eofbit` is set).
+   - `bool fail()`  
+     Returns true if an error has occurred (`failbit` or `badbit` are set).
+   - `bool bad()`  
+     Returns true if a serious error has occurred (`badbit` is set).
+   - `void clear()`  
+     Resets the state of `iostate`. Status is set to `goodbit`.
+   - `void clear(iostate f)`  
+     Resets the state of `iostate` and sets the status to `f`.
+   - `void setstate(iostate f)`  
+     The current state is combined with `f` using a bitwise OR.
+   - `iostate rdstate()`  
+     Returns the currently set status.

> **eofbit and failbit Set**
> 
> Usually, `failbit` is also set when `eofbit` is set. The reason is that the `eofbit` state is only set after an attempt is made to perform another action past the EOF. This also means that the next operation fails, and therefore `failbit` is set as well.

```
```cpp
// https://godbolt.org/z/exKMv8646
#include <fstream>
#include <iostream>
using std::cout; using std::cin; using std::ofstream;
void checkIOState(std::ios& stream) {
    if( stream.good() ) {
        cout << "All good\n";
    } else if( stream.bad() ) {
        cout << "Fatal error\n";
    } else if( stream.fail() ) {
        cout << "I/O error\n";
        if( stream.eof() ) {
            cout << "End of stream reached\n";
        }
    }
    stream.clear();
}
```
```