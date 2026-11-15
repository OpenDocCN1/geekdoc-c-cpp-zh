```
```cpp
int main(void)
{
    //Declare and initialize variables.
    double unknown[5]={5.4,7.2,7.9,7.4,5.1},
             known[5]={6.2,7.0,8.0,7.4,5.8};
    double distance(double hand_1[5],double hand_2[5]);

    // Compute and print distance.
    cout << "Distance: " << distance(unknown,known) << endl;

    // Exit program.
    return 0;
}
//---------------------------------------------
// This function computes the distance between two hand measurements.
double distance(double hand_1[5],double hand_2[5])
{
    // Declare variables.
    int k;
    double sum=0;

    // Compute sum of absolute value differences.
    for (k=0; k<=4; k++)
        sum = sum + fabs(hand_1[k]-hand_2[k]);

    // Return distance value.
    return sum;
}
//---------------------------------------------
```
```

# ## 5. TESTING

The test program has initialized the unknown and the known hand measurements to match those from the hand example. The output from the program is the following:

Distance: 1.8

The answer matches the hand example, so we can now test the program with additional data by changing the values in the test program. This would be a good problem to solve using hand measurements from the people in your class. Then take a new measurement from one of the students and compare the distance measurements with the entire class to see if the smallest distance is the one that it should match. Also, does it matter which order you use for the hand measurements in the function? It doesn't, but try switching the order to convince yourself. What if the distance measurement was just a sum, instead of an absolute value?