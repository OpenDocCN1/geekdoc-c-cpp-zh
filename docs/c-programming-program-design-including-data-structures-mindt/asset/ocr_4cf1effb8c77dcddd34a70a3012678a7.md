```
```cpp
object3.print();
object4.print();

object1.set("sphere", 4.5, 0);
object1.print();
```
```

17. What are the built-in operations on classes? (3)

18. What is the main difference between a struct and a class? (8)

19. Given the definition of the `class clockType` with constructors (as described in this chapter), what is the output of the following C++ code? (1, 2, 3, 5, 7)

```
```cpp
clockType myClock(10, 16, 59);
clockType yourClock;

myClock.incrementSeconds();
myClock.printTime();
cout << endl;

yourClock.setTime(23, 59, 29);
yourClock.printTime();
cout << endl;

yourClock.incrementMinutes();
yourClock.printTime();
cout << endl;
```
```

20. Consider the definition of the `class integerManipulation` given in Example 10-11. What is the output of the following C++ code? (1, 2, 3, 5, 7)

```
```cpp
integerManipulation number(3510862895423079232);

number.classifyDigits();
cout << number.getNum() << ": The number of digits---- "
     << endl;
cout << " Even: " << number.getEvensCount() << endl
     << " Zeros: " << number.getZerosCount() << endl
     << " Odd: " << number.getOddsCount() << endl;
```
```

21. Assume the definition of the `class personType` as given in this chapter. (1, 3)

+   a. Write a C++ statement that declares `student` to be a personType object, and initialize its first name to **"Buddy"** and last name to **"Arora"**.

+   b. Write a C++ statement that outputs the data stored in the object `student`.

+   c. Write a C++ statement that changes the first name of `student` to **"Susan"** and the last name to **"Gilbert"**.