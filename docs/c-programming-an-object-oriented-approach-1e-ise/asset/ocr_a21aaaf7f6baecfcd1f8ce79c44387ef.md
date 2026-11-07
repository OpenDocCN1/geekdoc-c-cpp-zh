# **Program 6.17**  Calculating a grade based on a score value (Continued)

```
```cpp
{
    cout << endl << "Result of the test." << endl;
    cout << "Score: " << score << " out of 100" << endl;
    cout << "Grade: ";
}
```
```

```
Run:
Enter a score between 0 and 100: 87
Result of the test.
Score: 87 out of 100
Grade: B

Run:
Enter a score between 0 and 100: 93
Result of the test.
Score: 93 out of 100
Grade: A
```

Figure 6.20 shows the communication between the *main* function and the three called functions.

When we analyze the small program in Figure 6.20, we find that the *main* function is responsible for coordinating the job of each of the other three functions. The first function, *getScore*, gets the data (*score*) from outside and gives it back to *main*. The second function, *findGrade*, receives the data (*score*) from *main*, processes it, and return the result (*grade*) back to *main*. The third function, *printResult*, receives two data items (*score* and *grade*) from *main* and sends them to the monitor.

Note that we have used the same name for the parameters and local variables that handle the score. We call all of them *score* without any confusion in the program. The reason is that they are in different territories (or scope, as we explain later). We have four storage locations called *score*, one in each entity. The ones in *getScore* and *main* are local variables; the ones in *findGrade* and *printResult* are parameters. We have also three storage locations named *grade*, two local variables and one parameter.

![](bbox=[0.299, 0.669, 0.865, 0.905])

**Figure 6.20**  Passing data between *main* and called functions