# Answers to Chapter Review for Chapter 16 1359

through the current function sequence of calls until it finds a try block that directly or indirectly calls the f2(). This might be in f1() or in a function called f1(), and so on. Once, execution goes to the next matching catch block, not to the first statement after the function call.

+   5. You should arrange the catch blocks in order, from most derived to least derived.

+   6. For Sample #1, if the condition is true pg points to a Superb object or to an object of any class descended from Superb. In particular, it is also true if pg points to a Magnificent object. In Sample #2, if the condition is true only for objects derived from Superb.

+   7. The dynamic_cast operator only allows upcasting in a class hierarchy, whereas a static_cast operator allows both upcasting and downcasting.The static_cast operator also allows conversions from enumeration types to integer types, and vice versa, between various numeric types.

# Answers to Chapter Review for Chapter 16

+   1. #include <string>
using namespace std;
class RQ1
private:
    string st; // a string object
public:
    RQ1() : st(**) {}
    RQ1(const char * s) : st(s) {}
    -RQ1() {};
    // more stuff
};

The explicit copy constructor, destructor, and assignment operator are no longer needed because the string object provides its own memory management.

+   2. You can assign one string object to another. A string object provides its own memory management that you normally don't have to worry about exceeding the capacity of its holder.

+   3. #include <string>
#include <ctype>
using namespace std;
void ToUpper(string & str)