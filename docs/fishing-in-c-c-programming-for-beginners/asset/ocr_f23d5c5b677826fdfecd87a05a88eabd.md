```
#include<fstream>
using namespace std;
int main()
{
    fstream fin;
    fin.open("example.txt",ios::in | ios::out);
    if(fin==NULL)
    {
        cout<<("Can't open the file");
        return -1;
    }
    fin<<"Hacking: Exploiting computer security with Aman";
    fin.seekp(3,ios::beg);
    int i=fin.tellp();
    cout<<i;
    fin.close();
    return 0;
}
```

Output

3

This program places the cursor at fifth offset then it returns its position. See, we open file in writing mode while using tellp

Note:- Remember the offset value can be negative, zero or positive integer.

# Using state flags

In addition to eof(), which checks if the end of file has been reached, other member functions exist to check the state of a stream (all of them return a bool value):