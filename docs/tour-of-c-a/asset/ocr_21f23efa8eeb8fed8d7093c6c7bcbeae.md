```
using namespace std;
using namespace ranges;

void f(vector<int>& & v)
{
    sort(v.begin(),v.end()); // error: ambiguous
    sort(v); // error: ambiguous
}
```