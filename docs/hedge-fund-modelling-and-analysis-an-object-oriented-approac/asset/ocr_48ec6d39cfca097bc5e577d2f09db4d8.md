```
cin.get();
return 0;
```

// Function definition
void swap(int &i, int &j)

```
{
    int t;
t=i;
i=j;
j=t;
}
```

![](bbox=[0.125, 0.355, 0.843, 0.611])

// ...
// Function prototype
void swap(const int &i, const int &j);

```
int main()
{
    SetConsoleTitle(L"Console Output");
```

//declare variables
int i = 1, j = 2;

```
cout << "\n" << " i = " << i << " j = " << j << "\n";
swap(i,j);
out << "\n" << " i = " << i << " j = " << j << "\n";
```