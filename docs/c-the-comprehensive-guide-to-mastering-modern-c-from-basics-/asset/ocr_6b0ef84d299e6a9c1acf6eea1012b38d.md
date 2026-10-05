These include guards prevent struct Person from being defined twice if you write #include "person.hpp" directly or indirectly twice. It is not necessary to use these guards, but it is very common practice.

> No “using” in the Header

As I mentioned at the beginning of the book, for the sake of brevity, I do not use using quite as you should in practice. In Figure 12.2, you can see it done correctly:

* Do not use global using in a header.
* In a *.cpp file, you can use using std::identifier.
* However, you should not use using namespace std; globally, not even in the *.cpp file.