# Program 7.5

```
#include <iostream>
using namespace std;

int findMax(int [], int);  // function prototype

int main()
{
    const int MAXELS = 5;
    int nums[MAXELS] = {2, 18, 1, 27, 16};

    cout << "The maximum value is " << findMax(nums, MAXELS) << endl;

    return 0;
}

// find the maximum value
int findMax(int vals[], int numels)
{
    int i, max = vals[0];

    for (i = 1; i < numels; i++)
        if (max < vals[i]) max = vals[i];

    return max;
}
```

The output displayed by Programs 7.4 and 7.5 is as follows:

```
The maximum value is 27
```

# EXERCISES 7.3

+   1. (Practice) The following declarations were used to create the grades array:
+      const int NUMGRADES = 500;
+      double grades[NUMGRADES];
+      Write two different function headers for a function named sortArray() that accepts the grades array as a parameter named inArray and returns no value.

+   2. (Practice) The following declarations were used to create the keys array:
+      const int NUMKEYS = 256;
+      char keys[NUMKEYS];