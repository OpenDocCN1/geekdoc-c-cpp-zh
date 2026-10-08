started. For example:

Click here to view code image

| Rand_int rnd(1,10); | Il make a random number generator for [1:10] |
| int x = rnd(); | Il x is a number in [1:10] |

So, could we get that very? We have to get something, that die(), combines an engine with a distribution inside a class Rand_int:

Click here to view code image

```
class Rand_int {
public:
    Rand_int(int low, int high) : dist(low,high) {} // Il an int
    int operator() { return dist(re); }
    void seed(int s) { re.seed(s); } // Il new random number seed
private:
    default_random_engine re;
    uniform_distribution<int> dist;
};
```

That definition is still "expert level", but that of Rand_int() is manageable in the first week of a C++ for novices. For example:

Click here to view code image

```
int main() {
    const int int max = 0;
    Rand_int rnd(0,max);

    vector<int> histogram(max+1);
    for (int i=0; i<200; ++i) // Il make a vector of appropriate size
        ++histogram[rnd(i)]; // Il fill histogram with the frequencies of numbers [0:max]

    for (int i = 0; i<histogram.size(); ++i) { // Il write out bar graph
        cout << i << "\t";
        for (int j=0; j<histogram[i]; ++j) cout << "*";
        cout << "\n";
    }
}
0
```

The output is a (reassuringly) uniform distribution (with reasonable statistical variation):

Click here to view code image

+   0 ********************
1 ********************
2 ********************
3 ********************
4 ********************
5 ********************
6 ********************
7 ********************
8 ********************
9 ********************

There is no standard graphics library for C++, so I use "ASCII graphics." Obviously, there are