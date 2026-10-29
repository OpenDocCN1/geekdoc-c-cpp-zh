# Display 3.8 Local Variables (part 1 of 2)

```
1 //Computes the average yield on an experimental pea growing patch.
2 #include <iostream>
3 using namespace std;

4 double estimateOfTotal(int minPeas, int maxPeas, int podCount);
5 //Returns an estimate of the total number of peas harvested.
6 //The formal parameter podCount is the number of pods.
7 //The formal parameters minPeas and maxPeas are the minimum
8 //and maximum number of peas in a pod.

9 int main( )
10 {
11     int maxCount, minCount, podCount;
12     double averagePea, yield;
13
14     cout << "Enter minimum and maximum number of peas in a pod: ";
15     cin >> minCount >> maxCount;
16     cout << "Enter the number of pods: ";
17     cin >> podCount;
18     cout << "Enter the weight of an average pea (in ounces): ";
19     cin >> averagePea;

20     yield =
21         estimateOfTotal(minCount, maxCount, podCount) * averagePea;

22     cout.setf(ios::fixed);
23     cout.setf(ios::showpoint);
24     cout.precision(3);
25     cout << "Min number of peas per pod = " << minCount << endl
26         << "Max number of peas per pod = " << maxCount << endl
27         << "Pod count = " << podCount << endl
28         << "Average pea weight = "
29         << averagePea << " ounces" << endl
30         << "Estimated average yield = " << yield << " ounces"
31         << endl;

32     return 0;
33 }

34 double estimateOfTotal(int minPeas, int maxPeas, int podCount)
35 {
36     double averagePea;
37     averagePea = (maxPeas + minPeas)/2.0;
38     return (podCount * averagePea);
39 }
```

This variable named averagePea is local to the main function.

This variable named averagePea is local to the function estimateOfTotal.