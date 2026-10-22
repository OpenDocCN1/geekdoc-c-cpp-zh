```
template<typename T>
class Outer {                  // #1
    public:
        template<typename U>
        class Inner {              // #2
            private:
                static int count;   // #3
        };
        static int code;            // #4
        void print() const {        // #5
            std::cout << "generic";
        }
};

template<typename T>
int Outer<T>::code = 6;         // #6
```