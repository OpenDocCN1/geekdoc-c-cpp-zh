# ### Listing 5-2: Seeing Another Function in Action

```
~~~cpp
#include <iostream>
#include <math.h>

using namespace std;

int main()
{
    double mynumber;
    mynumber = fabs(-23.87);
    cout << mynumber << endl;
    return 0;
}
~~~
```

This code declares a double variable called `mynumber`. Then it calls `fabs()`, passing it -23.87 and returning the value into `mynumber`. Next, it prints the value in `mynumber` to the console.

When you run this application, you see the following, which is the absolute value of -23.87:

23.87

# ## Passing a Variable

You can also pass the value of a variable into a function. The `fabs()` example in Listing 5-3 creates two variables: One is passed into the function, and the other receives the result of the function.

# ### Listing 5-3: Seeing Yet Another Function in Action

```
~~~cpp
#include <iostream>
#include <math.h>

using namespace std;

int main()
{
    double start;
    double finish;

    start = -253.895;
    finish = fabs(start);

    cout << finish << endl;
    return 0;
}
~~~
```

(We separated the parts of the code with blank lines to make it a little easier to follow.) This code first creates two variables; the first is called `start`, and the second is called `finish`. It then initializes `start` with a value of -253.895.