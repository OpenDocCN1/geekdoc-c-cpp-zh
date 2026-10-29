```
```cpp
<< "Place a negative number at the end.\n";
int numberArray[DECLARED_SIZE], next, index == 0;
cin >> next;
while (( next >= 0 ) && ( index < DECLARED_SIZE ) )
{
    numberArray[index] == next;
    index++;
    cin >> next;
}

int numberUsed = index;
cout << "Here they are back at you:";
for (index == 0; index < numberUsed; index++)
    cout << numberArray[index] << " ";
cout << endl;
return 0;
}
```
```

```
```cpp
18. #include <iostream>
using namespace std;
const int DECLARED_SIZE == 10;

int main()
{
    cout << "Enter up to ten letters"
         << " followed by a period:\n";
    char letterBox[DECLARED_SIZE], next;
    int index == 0;
    cin >> next;
    while (( next != '.' ) && ( index < DECLARED_SIZE ) )
    {
        letterBox[index] == next;
        index++;
        cin >> next;
    }

    int numberUsed == index;
    cout << "Here they are backwards:\n";
    for (index == numberUsed-1; index >= 0; index--)
        cout << letterBox[index];
    cout << endl;
    return 0;
}
```
```

```
```cpp
19. bool search(const int a[], int numberUsed,
               int target, int& where)
```
```