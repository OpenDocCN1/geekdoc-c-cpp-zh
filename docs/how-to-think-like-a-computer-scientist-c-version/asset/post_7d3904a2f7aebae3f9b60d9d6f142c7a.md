
## 9.4. PURE FUNCTIONS

```
if (time1.minute > time2.minute) return true;
if (time1.minute < time2.minute) return false;
```

```
if (time1.second > time2.second) return true;
return false;
}
```

What is the result of this function if the two times are equal? Does that seem like the appropriate result for this function? If you were writing the documentation for this function, would you mention that case specifically?

A second example is addTime, which calculates the sum of two times. For if it is 9:14:30, and your breadmaker takes 3 hours and 35 minutes, you could use addTime to figure out when the bread will be done.

Here is a rough draft of this function that is not quite right:

```
addTime(Time t1, Time t2) {
sum = ;
sum.hour = t1.hour + t2.hour;
sum.minute = t1.minute + t2.minute;
sum.second = t1.second + t2.second;
return sum;
}
```

Here is an example of how to use this function. If currentTime contains the current time and breadTime contains the amount of it takes for your breadmaker, then you could use addTime to figure out when the bread will be done.

```
Time currentTime = { 9, 14, 30.0 };
Time breadTime = { 3, 35, 0.0 };
Time doneTime = addTime(currentTime, breadTime);
printTime(doneTime);
```

The output of this program is 12:49:30, which is correct. On the other hand, there are cases where the result is not correct. Can you think of one?

The problem is that this function does not deal with cases where the number of seconds or minutes adds up more than 60. When that happens we have to "carry" the extra seconds into the minutes column, or extra minutes into the hours column.

Here's a second, corrected version of this function.

```
addTime(Time t1, Time t2) {
sum = ;
sum.hour = t1.hour + t2.hour;
sum.minute = t1.minute + t2.minute;
sum.second = t1.second + t2.second;

```
if (sum.second >= 60.0) {
  sum.second -= 60.0;
  sum.minute += 1;
}
if (sum.minute >= 60) {
  sum.minute -= 60;
  sum.hour += 1;
}
return sum;
}
```

Although it's correct, it's starting to get big. Later, I will suggest an alternate approach to this problem that will be much shorter.

This code demonstrates two operators we have not seen before, += and -=. These operators provide a concise way to increment and decrement variables. For example, the statement sum.second == 60.0; is equivalent to sum.second -= 60;

## 9.5 constant parameters

You might have noticed that the parameters for function after and addTime are passed by reference. Since these are pure functions, they do not modify the parameters they receive, so I could just well have passed them by value.

The advantage of passing by value is that the calling function and the callee are appropriately encapsulated—it is not possible for a change in one to affect the other, except by affecting the return value.

The other hand, passing by reference is usually more efficient, because it avoids copying the argument. there is a nice feature in C++, called const, can make reference parameters just safe as value parameters.

If you are writing a function and do not intend to modify a parameter, you can declare that it a constant reference parameter. The syntax looks like this:

```
void printTime(const Time& time) {
Time addTime(const Time& t1, const Time& t2) ...
```

I've included only the first line of the functions. If you tell the compiler you don't intend to change a parameter, it can help remind you. If you try to change one, you should get a compiler error, or at least a warning.

## 9.6 Modifiers

Of course, sometimes you want to modify one of the arguments. Functions that do are called modifiers.

## 9.7. FILL-IN FUNCTIONS

As an example of a modifier, consider increment, which adds a given number of seconds to a Time object. Again, a rough draft of this function looks like:

```
void increment(Time& time, double secs) {
  time.second += secs;

if (time.second >= 60.0) {
    time.second -= 60.0;
    time.minute += 1;
}
if (time.minute >= 60) {
    time.minute -= 60;
    time.hour += 1;
}
}
```

The first line performs the basic operation; the remainder deals with the special cases we saw before.

Is this function correct? What happens if the argument secs is much greater than 60? In that case, it is not enough to subtract 60 once; we have to keep doing until second is below 60. We can do that by replacing the if statements with while:

```
void increment(Time& time, double secs) {
  time.second += secs;

while (time.second >= 60.0) {
    time.second -= 60.0;
    time.minute += 1;
}
while (time.minute >= 60) {
    time.minute -= 60;
    time.hour += 1;
}
}
```

This solution is correct, but not very efficient. Can you think of a solution that does not require iteration?

## 9.7 Fill-in functions

Occasionally you will see functions like addTime written with a different interface (different arguments and return values). Instead of creating a new object every time addTime is called, we could require the caller to provide an "empty" object where addTime can store the result. Compare the following with the previous version:

```
void addTimeFill(const Time t1, const Time t2, Time sum) {
sum.hour = t1.hour + t2.hour;
sum.minute = t1.minute + t2.minute;
sum.second = t1.second + t2.second;

```
if (sum.second >= 60.0) {
sum.second -= 60.0;
sum.minute += 1;
}
if (sum.minute >= 60) {
sum.minute -= 60;
sum.hour += 1;
}
}
```

One advantage of this approach is that the caller has the option of reusing the same object repeated to perform a series of additions. This can be slightly more efficient, although it can be confusing enough to cause subtle errors. For the vast majority of programming, it is worth spending a long run time to avoid a lot of debugging time.

Notice that the first two parameters can be declared const, but the third cannot.

## 9.8 Which is best?

Anything that can be done with modifiers and fill-ins can also be done with pure functions. In fact, there are programming languages, called functional programming languages, that only allow pure functions. faster to develop and less error-prone than programs that use modifiers. Nevertheless, there are times when modifiers are convenient, and cases where functional programs are less efficient.

In general, I recommend that you write pure functions whenever it is reasonable to do so, and resort to modifiers only if there is a compelling advantage. This approach might be called a functional programming style.

## 9.9 Incremental development versus planning

In this chapter I have demonstrated an approach to program I refer to as rapid prototyping with iterative improvement. In each case, I wrote a rough draft (prototype) that performed the basic calculation, and tested it on a few cases, correcting flaws as I found. Although this approach can lead to code that is unnecessarily complicated—since it deals with many cases— and unreliable—since it is hard to know if you have found all the.

## 9.10 GENERALIZATION

An alternative is high-level planning, in which a little insight into the problem can make the programming much easier. In this case the insight is that Time is really a three-digit number in base 60! The second is the "ones column," the minute is the "60's column," and the hour is the "3600's column."

When we wrote addTime and increment, we were effectively doing addition in base 60, which is why we have to "carry" from one column to the next.

Thus an alternate approach to the whole problem is to convert Times into doubles and take advantage of the fact the computer already knows how to do arithmetic with doubles. Here is a function that converts a Time into a double:

```
double convertSeconds(const Time t) {
  int minutes = t.hour * 60 + t.minute;
  double seconds = minutes * 60 + t.second;
  return seconds;
}
```

Now all we need a way to convert from a double to a Time object:

```
Time makeTime(double secs) {
  Time time;
  time.hour = int (secs / 3600.0);
  secs -= time.hour * 3600.0;
  time.minute = int (secs / 60.0);
  secs -= time.minute * 60;
  time.second = secs;
  return time;
}
```

You might have to think a bit to convince yourself that the technique I am using to convert from one base to another is correct. Assuming you are convinced, we can use these functions to rewrite addTime:

```
Time addTime(const Time& t1, const Time& t2) {
  double seconds = convertSeconds(t1) + convertSeconds(t2);
  return makeTime(seconds);
}
```

This is much shorter than the original version, and it is much easier to demonstrate that it is correct (assuming, as usual, that the functions it calls are correct). As an exercise, rewrite increment the same way.

In some ways converting from base 60 to base 10 and back is harder than just dealing with times. Base conversion is more abstract; our intuition for dealing times is better.
