operator()'s second argument. The adaptor's members are typically very small so they are usually implemented inline.

The above application of the bind2nd adaptor has another important characteristic. Its return type is identical to the return type of the function object that it receives as its first argument, which is bool. Functions returning bool values are also called predicate functions. In the above application the bind2nd adaptor therefore becomes a predicate function itself.

The count_if generic algorithm visits all the elements in an iterator range, returning the number of times the predicate specified as its final argument returns true. Each of the elements of the iterator range is passed to this predicate, which is therefore a unary predicate. Through the binder the binary function object greater<> is adapted to a unary function object, that now compares each of the elements referred to by the iterator range to the reference string. Eventually, the count_if function is called like this:

```
~~~cpp
count_if(stringVector.begin(), stringVector.end(),
        bind2nd(greater<string>(), referenceString));
~~~
```

# 18.1.4.2 Negators

Negators are function adaptors converting the values returned by predicate function. Since there are unary and binary predicate functions, two negator function adaptors were predefined: not1 is the negator to use with unary predicates, not2 is the negator to with binary function objects.

Example: to count the number of persons in a vector<string> vector ordered alphabetically before (i.e., not exceeding) a certain reference text one of the following alternatives could be used:

+   - a binary predicate that directly offers the required comparison:
+   
+     ~~~cpp
+     count_if(stringVector.begin(), stringVector.end(),
+             bind2nd(less_equal<string>(), referenceText))
+     ~~~
+   
+   - not2 in combination with the greater<> predicate:
+   
+     ~~~cpp
+     count_if(stringVector.begin(), stringVector.end(),
+             bind2nd(not2(greater<string>()), referenceText))
+     ~~~
+   
+     Here not2 is used as it negates the truth value of a binary operator(), in this case the greater<string>::operator() member function.
+   
+   - not1 in combination with the bind2nd predicate:
+   
+     ~~~cpp
+     count_if(stringVector.begin(), stringVector.end(),
+             not1(bind2nd(greater<string>(), referenceText)))
+     ~~~
+   
+     Here not1 is used as it negates the truth value of a unary operator(), in this case the bind2nd function adaptor.

The use of negators is illustrated by the following program:

```
~~~cpp
#include <iostream>
#include <functional>
#include <algorithm>
#include <vector>
using namespace std;

int main(int argc, char **argv)
{
~~~
```