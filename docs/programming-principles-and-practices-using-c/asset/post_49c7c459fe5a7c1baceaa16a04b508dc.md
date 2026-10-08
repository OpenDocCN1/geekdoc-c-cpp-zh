
We tested this program by entering the hourly temperature values from the weather center in Lubbock, Texas, for February 16, 2004 (Texas still uses Fahrenheit):

```
-16.5,  -23.2,  -24.0,  -25.7,  -26.1,  -18.6,  -9.7,  -2.4,
  7.5,   12.6,   23.8,   25.3,   28.0,   34.8,  36.7,   41.5,
 40.3,   42.6,   39.7,   35.4,   12.6,    6.5,  -3.7,  -14.3
```

The output was

```
High temperature: 42.6
Low temperature: -26.1
Average temperature: 9.3
```

A naive programmer would conclude that the program works just fine. An irresponsible programmer would ship it to a customer. It would be prudent to test it again with another set of data. This time use the temperatures from July 23, 2004:

```
 76.5,  73.5,  71.0,  73.6,  70.1,  73.5,  77.6,  85.3,
 88.5,  91.7,  95.9,  99.2,  98.2, 100.6, 106.3, 112.4,
110.2, 103.6,  94.9,  91.7,  88.4,  85.2,  85.4,  87.7
```

This time, the output was

```
High temperature: 112.4
Low temperature: 0.0
Average temperature: 89.2
```

Oops! Something is not quite right. Hard frost (0.0°F is about −18°C) in Lubbock in July would mean the end of the world! Did you spot the error? Since `low_temp` was initialized at `0.0`, it would remain `0.0` unless one of the temperatures in the data was below zero.

## TRY THIS

![](img/e0ceba017429f80f5cf63e81a1e7ef4f_187_0.png)

> Get this program to run. Check that our input really does produce that output. Try to “break” the program (i.e., get it to give wrong results) by giving it other input sets. What is the least amount of input you can give it to get it to fail?

Unfortunately, there are more errors in this program. What would happen if all of the temperatures were below zero? The initialization for `high_temp` has the equivalent problem to **low_temp**: **high_temp** will remain at **0.0** unless there is a higher temperature in the data. This program wouldn’t work for the South Pole in winter either.

These errors are fairly typical; they will not cause any errors when you compile the program or cause wrong results for “reasonable” inputs. However, we forgot to think about what we should consider “reasonable.” Here is an improved program:

```cpp
int main()
{
    double sum = 0;
    double high_temp = -1000;    // initialize to impossibly low
    double low_temp = 1000;      // initialize to "impossibly high"
    int no_of_temps = 0;

    for (double temp; cin>>temp; ) {
        ++no_of_temps;            // count temperatures
        sum += temp;              // compute sum
        if (temp > high_temp) high_temp = temp;   // find high
        if (temp < low_temp) low_temp = temp;      // find low
    }

    cout << "High temperature: " << high_temp << "\n";
    cout << "Low temperature: " << low_temp << "\n";
    cout << "Average temperature: " << sum/no_of_temps << "\n";
}
```

Does it work? How would you be certain? How would you precisely define “work”? Where did we get the values **1000** and **–1000**? Remember that we warned about “magic constants” (§5.5.1). Having **1000** and **–1000** as literal values in the middle of the program is bad style, but are the values also wrong? Are there places where the temperatures go below –1000°F (–573°C)? Are there places the temperatures go above 1000°F (538°C)?

## TRY THIS

Look it up. Check some information sources to pick good values for the **min_temp** (the “minimum temperature”) and **max_temp** (the “maximum temperature”) constants for our program. Those values will determine the limits of usefulness of our program.

## 5.8 Estimation

Imagine you have written a program that does a simple calculation, say, computing the area of a hexagon. You run it and it gives the area -34.56. You just know that’s wrong. Why? Because no shape has a negative area. So, you fix that bug (whatever it was) and get 21.65685. Is that right? That’s harder to say because we don’t usually keep the formula for the area of a hexagon in our heads. What we must do before making fools of ourselves by delivering a program that produces ridiculous results is just to check that the answer is plausible. In this case, that’s easy. A hexagon is much like a square. We scribble our regular hexagon on a piece of paper and eyeball it to be about the size of a 3-by-3 square. Such a square has the area 9. Bummer, our 21.65685 can’t be right! So we work over our program again and get 10.3923. Now, that just might be right!

The general point here has nothing to do with hexagons. The point is that unless we have some idea of what a correct answer will be like - even ever so approximately - we don’t have a clue whether our result is reasonable. Always ask yourself this question:

- Is this answer to this particular problem plausible?

You should also ask the more general (and often far harder) question:

- How would I recognize a plausible result?

Here, we are not asking, “What’s the exact answer?” or “What’s the correct answer?” That’s what we are writing the program to tell us. All we want is to know that the answer is not ridiculous. Only when we know that we have a plausible answer does it make sense to proceed with further work.

*Estimation* is a noble art that combines common sense and some very simple arithmetic applied to a few facts. Some people are good at doing estimates in their heads, but we prefer scribbles “on the back of an envelope” because we find we get confused less often that way. What we call estimation here is an informal set of techniques that are sometimes (humorously) called *guesstimates* because they combine a bit of guessing with a bit of calculation.

## TRY THIS

![](img/e0ceba017429f80f5cf63e81a1e7ef4f_189_0.png)

Our hexagon was regular with 2cm sides. Did we get that answer right? Just do the “back of the envelope” calculation. Take a piece of paper and scribble on it. Don't feel that’s beneath you. Many famous scientists have been greatly admired for their ability to come up with an approximate answer using a pencil and the back of an envelope (or a napkin). This is an ability - a simple habit, really - that can save us a lot of time and confusion.

Often, making an estimate involves coming up with estimates of data that are needed for a proper calculation, but that we don't yet have. Imagine you have to test a program that estimates driving times between cities. Is a driving time of 15 hours and 33 minutes plausible for New York City to Denver? From London to Nice? Why or why not? What data do you have to "guess" to answer these questions? Often, a quick web search can be most helpful. For example, 2000 miles is not a bad guess on the road distance from New York City to Denver, and it would be hard (and illegal) to maintain an average speed of 130m/hr, so 15 hours is not plausible ($15 \times 130$ is just a bit less than 2000). You can check: we overestimated both the distance and the average speed, but for a check of plausibility we don't have to be exactly right; we just have to guess well enough.

## TRY THIS

> Estimate those driving times. Also, estimate the corresponding flight times (using ordinary commercial air travel). Then, try to verify your estimates by using appropriate sources, such as maps and timetables. We'd use online sources.

## 5.9 Debugging

When you have written (drafted?) a program, it'll have errors. Small programs do occasionally compile and run correctly the first time you try. But if that happens for anything but a completely trivial program, you should at first be very, very suspicious. If it really did run correctly the first time, go tell your friends and celebrate — because this won't happen every year.

So, when you have written some code, you have to find and remove the errors. That process is usually called *debugging* and the errors *bugs*. The term *bug* is often claimed to have originated from a hardware failure caused by insects in the electronics in the days when computers were racks of vacuum tubes and relays filling rooms. Several people have been credited with the discovery and the application of the word *bug* to errors in software. The most famous of those is Grace Murray Hopper, the inventor of the COBOL programming language (§22.2.2.2). However invented the term more than 50 years ago, *bug* is evocative and ubiquitous. The activity of deliberately searching for errors and removing them is called *debugging*.

Debugging works roughly like this:

- Get the program to compile.
- Get the program to link.
- Get the program to do what it is supposed to do.

Basically, we go through this sequence again and again: hundreds of times, thousands of times, again and again for years for really large programs. Each time
