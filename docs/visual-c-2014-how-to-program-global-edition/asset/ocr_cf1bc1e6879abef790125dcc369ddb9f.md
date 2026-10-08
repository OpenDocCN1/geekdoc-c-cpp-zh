# 10.5 Time Class Study: Overloaded Constructors 447

```
static void Main()\{
    var t1 = new Time2(); // 00:00:00
    var t2 = new Time2(); // 02:00:00
    var t3 = new Time2(2
```

t1: all arguments defaulted
00:00:00
12:00:00 AM

t2: hour specified; minute and second defaulted
02:00:00
2:00:00 AM

Fig.10.6 | Overloaded constructors used to initialize Time2 objects. (Part 2 of 3.)