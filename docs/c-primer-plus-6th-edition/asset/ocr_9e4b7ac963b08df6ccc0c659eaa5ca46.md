4. The personality member should be declared either as a character array or as a pointer-to-char. Or you could make it a String object or a string object. The declaration fails to make the methods public. Then there are several small errors. Here is a possible solution, with changes (other than deletions) in boldface:

```
#include <iostream>
#include <string>
using namespace std;
class nifty
{
    private: // optional
    char personality[40]; // provide array size
    int talents;
    public: // needed
    // methods
    nifty();
    nifty(const char * s);
    friend ostream &operator<<(ostream & os, const nifty & n);
};\ // note closing semicolon

nifty::nifty()
{
    personality[0] = '0';
    talents = 0;
}

nifty::nifty(const char * s)
{
    strcpy(personality, s);
    talents = 0;
}

ostream &operator<<(ostream & os, const nifty & n)
{
    os << n.personality << '\n';
    os << n.talent << '\n';
    return os;
}
```

Here is another possible solution:

```
#include <iostream>
#include <string>
using namespace std;
class nifty
{
    private: // optional
    char * personality; // create a pointer
```