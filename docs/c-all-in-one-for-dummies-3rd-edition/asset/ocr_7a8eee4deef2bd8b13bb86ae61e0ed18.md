You can see the type we used for the iterator, in this case called vectorloop. And you can see that we initialized it by calling begin(). We dereferenced it to get to the data itself, and then incremented vectorloop to get to the next item. And in the while loop we tested vectorloop against the results of end() to see whether we were all done.

![](bbox=[0.097, 0.22, 0.221, 0.306])

Many people seem to forget how to use iterators. We suggest keeping the Iterators example code in Listing 6-6 handy somewhere. (Print it and hang it on the wall, or save a copy in a directory on your hard drive where you can find it quickly, or maybe print it on really big paper and paste it to the front windshield of your car.) Then, if you forget how to put together a simple iterator, you can easily find the answer.

# ### Listing 6-6: Iterating

```
```cpp
#include <iostream>
#include <map>
#include <vector>

using namespace std;

int main()
{
    // Iterating through a map
    map<string, int> NumberWords;

    NumberWords["ten"] = 10;
    NumberWords["twenty"] = 20;
    NumberWords["thirty"] = 30;

    map<string, int>::iterator loop = NumberWords.begin();

    while (loop != NumberWords.end())
    {
        cout << loop->first << " ";
        cout << loop->second << endl;
        loop++;
    }

    // Iterating through a vector
    vector<string> Words;

    Words.push_back("hello");
    Words.push_back("there");
    Words.push_back("ladies");
    Words.push_back("and");
    Words.push_back("aliens");

    vector<string>::iterator vectorloop = Words.begin();

    while (vectorloop != Words.end())
    {
        cout << *vectorloop << endl;
        vectorloop++;
    }

    return 0;
}
```
```