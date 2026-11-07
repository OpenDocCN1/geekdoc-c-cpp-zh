# **Program 6.7** A guessing game (Continued)

```
```cpp
13 int high = 15;
14 int tryLimit = 5;
15 int guess;
16 // Generation of random number
17 srand(time(0));
18 int temp = rand();
19 int num = temp % (high - low + 1) + low;
20 // Guessing loop
21 int counter = 1;
22 bool found = false;
23 while (counter <= tryLimit && !found)
24 {
25     do
26     {
27         cout << "Enter your guess between 5 to 15 (inclusive): ";
28         cin >> guess;
29     } while (guess < 5 || guess > 15);
30 
31     if (guess == num)
32     {
33         found = true;
34     }
35     else if (guess > num)
36     {
37         cout << "Your guess was too high!" << endl;
38     }
39     else
40     {
41         cout << "Your guess was too low!" << endl;
42     }
43     counter++;
44 }
45 // Success response
46 if (found)
47 {
48     cout << "Congratulation: You found it. ";
49     cout << "The number was: " << num;
50 }
51 // Failure response
52 else
53 {
54     cout << "Sorry, you did not find it! ";
55     cout << "The number was: " << num;
56 }
```
```