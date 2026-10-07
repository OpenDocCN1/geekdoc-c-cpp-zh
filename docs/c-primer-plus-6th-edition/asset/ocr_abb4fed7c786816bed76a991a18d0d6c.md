# 576 Chapter 11 Working with Classes

```
minutes += m;
hours += minutes / 60;
minutes %= 60;
}
void Time::AddHr(int h)
{
    hours += h;
}
void Time::Reset(int h, int m)
{
    hours = h;
minutes = m;
}
Time::operator+(const Time & t) const
{
    Time sum;
sum.minutes = minutes + t.minutes;
sum.hours = hours + t.hours + sum.minutes / 60;
sum.minutes %= 60;
    return sum;
}
Time::operator-(const Time & t) const
{
    Time diff;
    int tot1, tot2;
tot1 = t.minutes + 60 * t.hours;
tot2 = minutes + 60 * tot1;
diff.minutes = (tot2 - tot1) % 60;
diff.hours = (tot2 - tot1) / 60;
    return diff;
}
Time::operator*(double mult) const
{
    Time result;
    long totalminutes = hours * mult * 60 + minutes * mult;
result.hours = totalminutes / 60;
result.minutes = totalminutes % 60;
    return result;
}
void Time::Show()
{
    std::cout << hours << " hours, " << minutes << " minutes";
}
```