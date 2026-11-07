# Program 19.13  Grouping charity donations (Continued)

```
```cpp
for (int i = 0; i < 50; i++)
{
    num = rand();
    donation = num % (50 - 0 + 0) + 0;
    switch (donation / 10)
    {
        case 0: queue1.push(donation);
            break;
        case 1: queue2.push(donation);
            break;
        case 2: queue3.push(donation);
            break;
        case 3: queue4.push(donation);
            break;
        case 4: queue5.push(donation);
            break;
    }
}
// Printing the donations in each group
cout << "Donations between 00 and 09: ";
print(queue1);
cout << "Donations between 10 and 19: ";
print(queue2);
cout << "Donations between 20 and 29: ";
print(queue3);
cout << "Donations between 30 and 39: ";
print(queue4);
cout << "Donations between 40 and 49: ";
print(queue5);
return 0;
}
// Definition of the print function
void print(queue<int> queue)
{
    while (!queue.empty())
    {
        cout << queue.front() << " ";
        queue.pop();
    }
    cout << endl;
}
```
```

```
```text
Run:
Donations between 00 and 09:  3  1  3  7  9  1  8  8  9  7  4  3
Donations between 10 and 19:  18  14  13  15  16  15
Donations between 20 and 29:  23  26  28  29  23  21  26  21  22  27  28  23
Donations between 30 and 39:  32  31  39  39  39  34  30  38  30  36  32
Donations between 40 and 49:  41  49  49  43  47  43  45  46  41
```
```