# DISPLAY 14.2 Iterative Version of the Function in Display 14.1

```
//Uses iostream:
void writeVertical(int n)
{
    int tensInN = 1;
    int leftEndPiece = n;
    while (leftEndPiece > 9)
    {
        leftEndPiece = leftEndPiece/10;
        tensInN = tensInN * 10;
    }
    //tensInN is a power of ten that has the same number
    //of digits as n. For example, if n is 2345, then
    //tensInN is 1000.
    for (int powerOf10 = tensInN;
        powerOf10 > 0; powerOf10 = powerOf10/10)
    {
        cout << (n/powerOf10) <<endl;
        n = n % powerOf10;
    }
}
```

A recursively written function will usually run slower and use more storage than an equivalent iterative version. Although the iterative version of writeVertical given in Display 14.2 looks like it uses more storage and does more computing than the recursive version in Display 14.1, the two versions of writeVertical actually use comparable storage and do comparable amounts of computing. In fact, the recursive version may use more storage and run somewhat slower, because the computer must do a good deal of work manipulating the stack in order to keep track of the recursion. However, since the system does all this for you automatically, using recursion can sometimes make your job as a programmer easier and can sometimes produce code that is easier to understand. As you will see in the examples in this chapter and in the Self-Test Exercises and Programming Projects, sometimes a recursive definition is simpler and clearer; other times, an iterative definition is simpler and clearer.

# SELF-TEST EXERCISES

+   6. If your program produces an error message that says stack overflow, what is a likely source of the error?

+   7. Write an iterative version of the function cheers defined in Self-Test Exercise 1.