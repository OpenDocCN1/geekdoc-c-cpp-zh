```
class Clock
{
public:
    Clock(); //constructor
    void SetTime(int newH, int newM, int newS);
    void ShowTime();
    ~Clock()
private:
    int Hour, Minute, Second;
};
```

Generally speaking, if we want the program to do some work automatically before the object disappears (without manually calling a function), we can write the work into the destructor.

# 4.3.4 Program Instance

**Example 4.3:** Budget for rebuilding a pool with *Circle* class. Fencing costs $35$/m and an aisle costs $20/m². The width of the aisle is 3 meters, and the radius of the pool will be input from the keyboard. Write a program to compute and output the costs of the aisle and the fence.

The pool and the fence can be viewed as two concentric circles. The circumference of the larger circle is the length of the fence, the area of the circular ring is the difference between the larger circle's area, and the smaller circle's area. We can define a class Circle to describe this problem: the radius of the circle is a private data member, and the function of class Circle is to compute the girth and the area of the circle. We use two objects to represent the fence and pool, and then we can get the area of the aisle and the girth of the fence. Given the unit prices, we can get the budget of the whole project. Let’s see the implementation of the program:

![](bbox=[0.181, 0.715, 0.416, 0.878])

**Fig. 4.2:** The pool.