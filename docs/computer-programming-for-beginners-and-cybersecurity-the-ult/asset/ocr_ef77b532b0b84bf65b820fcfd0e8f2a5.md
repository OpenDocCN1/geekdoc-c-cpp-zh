```
using namespace std;
int main()
{
    vector<int> v;
    for(int i = 0; i < 10; i++)
        v.push_back(i);
    int a = 5;
    vector<int>::iterator it;
    it = find(v.begin(),v.end(),a);
    if(it != v.end()) {
        cout << "found " << a<< endl;
    }
    else {
        cout << "could not find " << a << endl;
    }
    int c = count(v.begin(), v.end(), 6);
    cout<<"Number of 6 stored in vector:" << c;
    return 0;
}
```

Output: found 5

Number of 6 stored in vector: 1

+   - For each()