```
#include<iostream>//Required for cout
#include<cmath>//Required for sqrt()
using namespace std;
int main()
{
    // Declare and initialize objects.
    double x1(1), y1(5), x2(4), y2(7),
           side1, side2, distance;
    // Compute sides of a right triangle.
    side1 = x2 - x1;
    side2 = y2 - y1;
    distance = sqrt(side1*side1 + side2*side2);
    // Print distance.
    cout << "The distance between the two points is"
         << distance << endl;
    // Exit program.
    return 0;
}
/******************************************************************/
```

# ## 5. TESTING

The final step in our problem-solving process is testing the solution. We should first test the solution with the data from the hand example because we have already computed the solution. When the C++ statements in this solution are executed, the computer displays the following output:

The distance between the points is 3.60555

This output matches the value that we calculated by hand. If the C++ solution did not match the hand solution, then we should review both solutions to find the error. Once the solution works for the hand example, we should also test it with additional sets of data to be sure that the solution works for other valid sets of data.

The set of steps demonstrated in this example are used in developing the programs in the Problem Solving Applied sections in the chapters that follow.

# ## SUMMARY

A brief history of the development of the digital computer was provided, followed by a group of outstanding recent engineering achievements to demonstrate the diversity of engineering applications, and the impact of computers in engineering. We also discussed some of the non-technical skills required to be a successful engineer. Because the solutions to most engineering problems will be by computer, we presented a summary of the components of a computer system, from computer hardware to computer software and the importance of learning the new terminology. We also discussed number systems and data representation and introduced