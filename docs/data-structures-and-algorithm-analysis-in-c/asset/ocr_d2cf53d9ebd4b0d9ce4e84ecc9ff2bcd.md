```
1 #include "MemoryCell.h"
2 
3 /**
4  * Construct the MemoryCell with initialValue.
5  *
6  */
7 template <typename Object>
8 MemoryCell<Object>::MemoryCell( const Object & initialValue )
9   : storedValue{ initialValue }
10 {
11 }
12 
13 /**
14  * Return the stored value.
15  *
16  */
17 template <typename Object>
18 const Object & MemoryCell<Object>::read( ) const
19 {
20   return storedValue;
21 }
22 
23 /**
24  * Store x.
25  *
26  */
27 template <typename Object>
28 void MemoryCell<Object>::write( const Object & x )
29 {
30   storedValue = x;
31 }
```

# **Figure A.2 MemoryCell class template implementation**

be done for classes. Thus, both Figure A.1 and Figure A.2 would be exactly as currently shown. The header file would not have an include directive to read the implementation. The main routine would only have an include directive for the header file. Figure A.3 shows a typical test program. If we compile both .cpp files, we find that the instantiated member functions are not found. We fix the problem by creating a separate file that contains explicit instantiations of the MemoryCell for the types we use. An example of the explicit instantiations is shown in Figure A.4. This file is compiled as part of the project, and the template implementation file (Figure A.2) is not compiled as part of the project. We have had success using this technique with several older compilers. The downside is that all of the template expansions have to be listed by the programmer, and when the class template uses other class templates, sometimes those have to be listed, too. The advantage is that if the implementation of the member functions in MemoryCell changes, only MemoryCellExpand.cpp needs to be recompiled.