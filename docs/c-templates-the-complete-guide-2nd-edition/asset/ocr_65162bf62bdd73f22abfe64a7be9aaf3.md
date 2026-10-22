```
template<>
    template<>
    class Outer<char>::Inner<wchar_t> {
        public:
            enum { count = 1 };
    };

// the following is not valid C++:
// template<> cannot follow a template parameter list
template<typename X>
template<> class Outer<X>::Inner<void>; // ERROR
```