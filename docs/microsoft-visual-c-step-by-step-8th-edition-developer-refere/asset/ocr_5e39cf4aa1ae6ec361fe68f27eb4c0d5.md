```
int number = int.MaxValue;
checked
{
    int willThrow = number++;
    Console.WriteLine("this won’t be reached");
}
```