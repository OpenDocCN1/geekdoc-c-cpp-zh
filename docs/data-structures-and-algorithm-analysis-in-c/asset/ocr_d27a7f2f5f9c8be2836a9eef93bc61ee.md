```
1 #include "MemoryCell1.h"
2 #include <iostream>
3
4 using namespace std;
5
6 int main( )
7 {
8   MemoryCell<int> m1;
9   MemoryCell<double> m2( 3.14 );
10
11   m1.setValue( 37 );
12   m2.setValue( m2.getValue( ) * 2 );
13
14   cout << m1.getValue( ) << endl;
15   cout << m2.getValue( ) << endl;
16
17   return 0;
18 }
```

**Figure A.3** Using the MemoryCell class template

```
1 #include "MemoryCell1.cpp"
2
3 template class MemoryCell<int>;
4 template class MemoryCell<double>;
```

**Figure A.4** Instantiation file MemoryCellExpand.cpp