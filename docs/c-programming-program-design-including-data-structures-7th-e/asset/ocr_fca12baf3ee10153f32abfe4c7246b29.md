```
```cpp
if (sec < 10)
    cout << "0";
cout << sec;
}
```
```

```
```cpp
void clockType::incrementHours()
{
    hr++;
    if (hr > 23)
        hr = 0;
}
```
```

```
```cpp
void clockType::incrementMinutes()
{
    min++;
    if (min > 59)
    {
        min = 0;
        incrementHours(); //increment hours
    }
}
```
```

```
```cpp
void clockType::incrementSeconds()
{
    sec++;

    if (sec > 59)
    {
        sec = 0;
        incrementMinutes(); //increment minutes
    }
}
```
```

From the definitions of the functions incrementMinutes and incrementSeconds, it is clear that a member function of a class can call other member functions of the class.

The function equalTime has the following definition:

```
```cpp
bool clockType::equalTime(const clockType& otherClock) const
{
    return (hr == otherClock.hr
            && min == otherClock.min
            && sec == otherClock.sec);
}
```
```

Let us see how the member function equalTime works.

Suppose that myClock and yourClock are objects of type clockType, as declared previously. Further suppose that we have myClock and yourClock, as shown in Figure 10–5.