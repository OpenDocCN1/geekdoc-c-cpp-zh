OUTPUT :
Hello from inline show

EXPLANATION : The function show is inline so when it is called in the main it is simply expanded in the main. That is, all the statements written in the function show appear at the place of function call. Here we are having just one cout statement so it appear through we have written cout statement within main itself similar to macro.

```
/*PROG 5.18 DEMO OF INLINE FUNCTION VER 2*/

#include <iostream.h>
#include <conio.h>

inline void show( );

void main( )
{
    show( );
}
inline void show( )
{
    cout << "Hello from inline show\n";
}

OUTPUT :
Hello from inline show
```

EXPLANATION : An inline function has to be defined before it can be used. But the above program works fine in Visual Studio C++ compiler. However, in Turbo C 3.0 on executing the program makes system halts. There is no compilation error in Turbo C3.0.

```
/*PROG 5.19 SQUARE OF A NUMBER USING INLINE FUNCTION VER 1*/

#include <iostream.h>
#include <conio.h>

inline int square(int x)
{
    return x*x;
}

void main( )
```