# STEP 6

With the countdown code, don’t forget to include the windows.h library, so you can use the Sleep command. Build and run the code; in the command console you can see the numbers 10 to 1 countdown in one second increments, until it reaches zero and Blast Off! appears.

![](bbox=[0.066, 0.207, 0.491, 0.35])

# STEP 7

Naturally you can include a lot more content into a for loop, including some user input:

```
```cpp
int i, n, fact = 1;

cout << “Enter a whole number: “;
cin >> n;

for (i = 1; i <= n; ++i) {
    fact *= i;
}

cout<< “\nFactorial of “ << n <<” = “<< fact << endl;

return 0;
```
```

![](bbox=[0.066, 0.547, 0.491, 0.734])

# STEP 8

The code from step 7, when built and run, asks for a number, then displays the factorial of that number through the for loop. The user’s number is stored in the integer n, followed by the integer I which is used to check if the condition is true or false, adding 1 each time and comparing it to the user’s number, n.

![](bbox=[0.066, 0.839, 0.491, 0.951])

# STEP 9

Here’s an example of a for loop displaying the multiplication tables of a user inputted number. Handy for students:

```
```cpp
{
    int n;

    cout << “Enter a number to view its times table: “;
    cin >> n;

    for (int i = 1; i <= 12; ++i) {
        cout << n << “ x “ << i << “ = “ << n * i << endl;
    }

    return 0;
}
```
```

![](bbox=[0.509, 0.35, 0.933, 0.555])

# STEP 10

The value of the integer i can be expanded from 12 to whatever number you want, displaying a very large multiplication table in the process (or a small one). Of course the data type within a for loop doesn’t have to be an integer, as long as it’s valid, it works.

```
```cpp
for ( float i = 0.00; i < 1.00; i += 0.01)
{
    cout << i << endl;
}

return 0;
```
```

![](bbox=[0.509, 0.731, 0.933, 0.951])