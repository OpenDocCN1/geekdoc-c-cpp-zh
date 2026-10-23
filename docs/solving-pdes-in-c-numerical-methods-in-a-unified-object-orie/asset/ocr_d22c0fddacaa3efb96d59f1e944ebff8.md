In the next section we provide a more complete version of this template class with many useful functions, from which both two-dimensional and three-dimensional points can be obtained as special cases.

# 2.18 Example: The Vector Object

In this section, we present the "vector<T,N>" template class that implements an N-dimensional vector space, in which each vector has N components of type 'T'. The arithmetic operators implemented in this class provide a useful and convenient framework to handle vectors. The two-dimensional and three-dimensional point objects are also obtained as a special case.

Most operators and functions, except very short ones, are only declared inside the class block below, and their actual definition is placed outside it later on. The prefix "vector<T,N>::" that precede a function name indicates that a member function is defined. The words "template<class T, int N>" that precede the definition of a function indicate that this is a template function that uses the as yet unspecified type 'T' and integer 'N':

```
#include<stdio.h>
template<class T, int N> class vector{
    T component[N];
public:
    vector(const T&);
    vector(const vector&);
    const vector& operator=(const vector&);
    const vector& operator=(const T&);
```

So far, we have only declared the constructor, copy constructor, and assignment operators with scalar and vector arguments. The actual definitions will be provided later. Next, we define the destructor. Actually, the destructor contains no command. The actual destruction is done by the default destructor invoked at the end of the function:

```
~vector(){
} // destructor
```

Because the components in the vector are private class members, we need public functions to access them. These functions can then be called even from nonmember and nonfriend functions:

```
const T& operator[](int i) const{
    return component[i];
} //read ith component

void set(int i,const T& a){
    component[i] = a;
} // change ith component
```

Here we declare more member arithmetic operators, to be defined later: