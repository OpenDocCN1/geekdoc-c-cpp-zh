```
```cpp
set_pc(four);
// ill-advised assignment
accumulate(dup, five) = four;
std::cout << "Displaying dup after ill-advised assignment:\n";
display(dup);
return 0;
}

void display(const free_throws & ft)
{
    using std::cout;
    cout << "Name: " << ft.name << '\n';
    cout << "  Made: " << ft.made << '\t';
    cout << "Attempts: " << ft.attempts << '\t';
    cout << "Percent: " << ft.percent << '\n';
}
void set_pc(free_throws & ft)
{
    if (ft.attempts != 0)
        ft.percent = 100.0f * float(ft.made)/float(ft.attempts);
    else
        ft.percent = 0;
}

free_throws & accumulate(free_throws & target, const free_throws & source)
{
    target.attempts += source.attempts;
    target.made += source.made;
    set_pc(target);
    return target;
}
```
```

Here is the program output:

```
```text
Name: Ifelsa Branch
  Made: 13    Attempts: 14    Percent: 92.8571
Name: Throwgoods
  Made: 13    Attempts: 14    Percent: 92.8571
Name: Throwgoods
  Made: 23    Attempts: 30    Percent: 76.6667
Name: Throwgoods
  Made: 35    Attempts: 48    Percent: 72.9167
Displaying team:
Name: Throwgoods
  Made: 41    Attempts: 62    Percent: 66.129
Displaying dup after assignment:
Name: Throwgoods
```
```