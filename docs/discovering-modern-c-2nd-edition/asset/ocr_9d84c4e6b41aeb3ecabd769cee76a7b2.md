```
void increment(int x)
{
    x++;
}

int main()
{
    int i = 4;
    increment(i);     // Does not increment i
    cout << "i is " << i << '\n';
}
```