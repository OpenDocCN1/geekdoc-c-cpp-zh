+   4. Which of the following is true with respect to memory allocation? (L2)
+   (a) New must be used with free always, if not it would throw an exception.
+   (b) New must be used with delete always, if not it would throw an exception.
+   (c) New need not be associated with delete.
+   (d) Though not mandatory, it is a good practice to use delete.

**Answer:** 'b', 'c' and 'd'

+   5. What is the output of the following code? (L3)

```
#include <iostream>
using namespace std;
int main ()
{
    int *pointer;
    pointer = new int ;
    cout <<"return value" <<pointer <<"\n";
    free pointer;
    return 0;
}
```

+   (a) An address would be returned if space is available.
+   (b) Compilation error as free cannot be used in this code.
+   (c) Syntax error.
+   (d) No output. No error.

**Answer** (b) Usage of free is not allowed in this context.

+   6. What is the output of the following code? (L3)

```
#include <iostream>
using namespace std;
int main ()
{
    int *pointer;
    pointer = new int;
    cout <<"return value" <<pointer <<"\n";
    delete pointer;
    return 0;
}
```

+   (a) An address would be returned if space is available and delete will be executed perfectly.
+   (b) Compilation error as delete cannot be used in this code.
+   (c) Syntax error.
+   (d) No output. No error.

**Answer:** (a) is the correct answer as it has been used perfectly.

+   7. What is the output of the following code? (L3)

```
#include <iostream>
using namespace std;
int main ()
{
    int *pointer;
    pointer = new int [2];
    cout <<"return value" <<pointer <<"\n";
    delete [2] pointer;
    return 0;
}
```

+   (a) An address would be returned if space is available and delete will be executed perfectly.
+   (b) Compilation error.
+   (c) Syntax error.
+   (d) No output. No error.

**Answer:** (b) is the answer. Type 'int' argument given to 'delete' is the error.

+   8. What is the output of the following code? (L3)

```
#include <iostream>
using namespace std;
int main ()
{
    int *pointer;
    pointer = new int [2];
    cout <<"return value" <<pointer <<"\n";
    delete [] pointer;
    return 0;
}
```