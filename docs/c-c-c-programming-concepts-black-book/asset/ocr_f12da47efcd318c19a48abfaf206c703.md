# Chapter B

2. Write a C++ program for std::find and std::find_if for finding information in vectors.

```
```cpp
#include <iostream>
#include <vector>
#include <algorithm> //needed for std::find
using namespace std;

bool findodd(int i)
{
    return ((i%2)==1);
}

int main()
{
    vector<int> v1;
    v1.push_back(66);
    v1.push_back(767);
    v1.push_back(348);
    v1.push_back(989);
    v1.push_back(4648);
    v1.push_back(96321);
    v1.push_back(878);
    v1.push_back(765);

    //Demonstrating Find – Find the number 4648 and its position, if present

    vector<int>::const_iterator it = find(v1.begin(), v1.end(), 4648);
    if(it != v1.end())
    {
        cout<<"Found: "<<it<<endl;
        cout<<"Position = "<<it - v1.begin() + 1<<endl;
    }
    else
    {
        cout<<"Not Found"<<endl;
        cout<<"Position = -1"<<endl;
    }

    //Demonstrating Find IF – Find the first odd number and its position

    it = find_if(v1.begin(), v1.end(), findodd);
    if(it != v1.end())
    {
        cout<<"Found: "<<it<<endl;
        cout<<"Position = "<<it - v1.begin() + 1<<endl;
    }
    else
    {
        cout<<"No Odd Numbers Found"<<endl;
        cout<<"Position = -1"<<endl;
    }
    system("pause");
    return 0;
}
```
```