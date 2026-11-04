```
{
    int i, len;
    string s1, s2, s3;
    cout << "Enter strings: ";
    cin >> s1 >> s2;
    s3 = s1+s2;
    s3.append("end");
    len = s3.length();
    cout << "L:" << len << " S:" << s3 << endl;
    i = s3.find('a');
    if(i == -1)
        cout << "Not found\n";
    else
        cout << "Found in position:" << i+1 << endl;
    s3.resize(2*len, s1[0]);
    s3.erase(0, 3);
    cout << s3 << endl;
    return 0;
}
```

Another example of an often used standard class is the class template vector. It is used as an array. The main advantage over an ordinary array is that its size may be modified at runtime. For example:

```
#include <iostream>
#include <vector>
using namespace std;

int main()
{
    int i;
    vector<int> arr(3); /* Create a vector of integers with three elements. In another example, we could use a class instead of int and create a vector of objects of that class. */
    for(i = 0; i < arr.size(); i++)
    {
        arr[i] = 10+i;
        cout << arr[i] << ' ';
    }
    arr.push_back(20); /* Add elements at the vector end and allocate memory if necessary. */
    arr.push_back(30);
    for(i = 0; i < arr.size(); i++)
        cout << arr[i] << ' ';
    return 0;
}
```

First, the program displays the values of three elements: 10 11 12. Next, it displays the values of five elements: 10 11 12 20 30.