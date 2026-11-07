```
```cpp
double poolCapacity(double len, double wid, double dep)
{
    double volume;
    double poolWaterCapacity;

    volume = len * wid * dep;
    poolWaterCapacity = volume * GALLONS_IN_A_CUBIC_FOOT;

    return poolWaterCapacity;
}

void poolFillTime(double len, double wid, double dep,
                  double &rate, int &ftime)
{
    double poolWaterCapacity;

    poolWaterCapacity = poolCapacity(len, wid, dep);
    ftime = static_cast<int> (poolWaterCapacity / rate + 0.5);
}

void print(int ftime)
{
    cout << "The time to fill the pool is approximately: "
         << ftime / 60 << " hour(s) and " << ftime % 60
         << " minute(s)." << endl;
}
```
```

**Sample Run:** In this sample run, the user input is shaded.

Enter the length, width, and the depth of the pool, (in feet): `30 15 10`

Enter the rate of the water, (in gallons per minute): `100`

The time to fill the pool is approximately: 5 hour(s) and 37 minute(s).

As you can see, the program contains the function *poolCapacity* to find the amount of water needed to fill the pool, the function *poolFillTime* to find the time to fill the pool, and some other functions. Now, to calculate the time to fill the pool, you must know the amount of water needed and the rate at which the water is released in the pool. Because the results of the function *poolCapacity* are needed in the function *poolFillTime*, the function *poolFillTime* cannot be tested alone. Does this mean that we must write the functions in a specific order? Not necessarily, especially when different people are working on different parts of the program. In situations such as these, we use function stubs. A **function stub** is a function that is not fully coded. For a void function, a function stub might consist of only a function header and a set of empty braces, {}; and for a value-returning function it might contain only a return statement with a plausible and easy to use return value. For example, the function stub for the function *poolCapacity* can be: