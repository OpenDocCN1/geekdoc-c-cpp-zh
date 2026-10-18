# SELF-TEST EXERCISES

19. Give a type definition for a structure called Score that has two member variables called homeTeam and opponent. Both member variables are of type int. Declare an array called game that is an array with ten elements of type Score. The array game might be used to record the scores of each of ten games for a sports team.

20. Write a program that reads in five amounts of money, doubles each amount, and then writes out the doubled values to the screen. Use one array with Money as the base type. (Hint: Use Display 11.9 as a guide, but this program will be simpler than the one in Display 11.9.)

# Arrays as Class Members

You can have a structure or class that has an array as a member variable. For example, suppose you are a speed swimmer and want a program to keep track of your practice times for various distances. You can use the structure myBest (of the type Data given next) to record a distance (in meters) and the times (in seconds) for each of ten practice tries swimming that distance:

```
struct Data
{
    double time[10];
    int distance;
};
Data myBest;
```

The structure myBest, declared above, has two member variables: One, named distance, is a variable of type int (to record a distance); the other, named time, is an array of ten values of type double (to hold times for ten practice tries at the specified distance). To set the distance equal to 20 (meters), you can use the following:

```
myBest.distance = 20;
```

You can set the ten array elements with values from the keyboard as follows:

```
cout << "Enter ten times (in seconds):\n";
for (int i = 0; i < 10; i++)
    cin >> myBest.time[i];
```

The expression myBest.time[i] is read left to right: myBest is a structure; myBest.time is the member variable named time. Since myBest.time is an array, it makes sense to add an index. So, the expression myBest.time[i] is the i th indexed variable of the array myBest.time. If you use a class rather than a structure type, then you can do all your array manipulations with member functions and avoid such confusing expressions. This is illustrated in the following Programming Example.