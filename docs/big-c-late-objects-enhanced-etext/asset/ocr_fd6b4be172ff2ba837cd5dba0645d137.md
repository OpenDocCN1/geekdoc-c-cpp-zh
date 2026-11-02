```
```c
for (int j = 0; j < size; j++)
{
    int value = values[j];
    counters[value]++;
}

/**
 * Prints a table of die value counters.
 * @param faces the number of faces of the die
 * @param counters an array of counters of length faces + 1.
 * counters[0] is not printed.
 */
void print_counters(int faces, int counters[])
{
    for (int i = 1; i <= faces; i++)
    {
        cout << i << ": " << counters[i] << endl;
    }
}

int main()
{
    const int FACES = 6;
    int counters[FACES + 1];
    const int NUMBER_OF_TOSSES = 12;
    int tosses[NUMBER_OF_TOSSES];

    generate_test_values(tosses, NUMBER_OF_TOSSES, FACES, counters);
    count_values(tosses, NUMBER_OF_TOSSES, FACES, counters);
    print_counters(FACES, counters);
    return 0;
}
```
```