# Recursion Iteration

Recursion is not absolutely necessary. In fact, some programming languages do not allow it. Any task that can be accomplished using recursion can be done in some other way without using recursion. For example, Display 13.2 contains a nonrecursive version of the function in Display 13.1. The nonrecursive version of a function typically uses a loop (or loops) of some sort in place of recursion. For this reason, the nonrecursive version is usually referred to as an iterative version. If definition of the function vertical in Display 13.1 is replaced by the version in Display 13.2, the output will be the same. As is true in this case, a recursive version of a function can be much simpler and more elegant than an iterative version so a gain in efficiency is not always preferable.

Display 13.2 Iterative Version of the Function in Display 13.1

```
//Uses iostream:
void writeVertical(int n)
{
    int nsTens = 1;
    int leftPiece = n;
    while (leftPiece > 9)
    {
        leftPiece = leftPiece / 10;
        nsTens = nsTens * 10;
    }
    //nsTens is a power of ten that has the same number
    //of digits as n. For example, if n is 2,345, then
    //nsTens = 1000;

    for (int powerOf10 = 1; powerOf10 < nsTens; powerOf10 *= 10)
    {
        cout << (n / powerOf10) << endl;
        n = n % powerOf10;
    }

```

Modern compilers will convert certain recursive functions to equivalent iterative ones automatically for you. A function that uses tail recursion has the property that no further computation occurs after the recursive call; the function immediately returns. In the next section, when we use recursive functions with a return value, a function is tail if the value of a recursive call is returned without modification. In such cases, a tail recursion can be easily converted to an equivalent iterative solution. Check your compiler’s documentation and optimization flags to see if this operation is available.