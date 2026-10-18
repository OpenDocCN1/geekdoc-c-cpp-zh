```
#include <iostream.h>
class Room
{
int length;
int width;
public:
Room( )
{
length = 0;
width = 0;
}
Room(int value=8)
length = width = 8;
void display()
cout << length << ' ' << width;
}
};
void main( )
{
Room objRoom1;
objRoom1.display( );
}
```

6.3 Identify the error in the following program.

```
#include <iostream.h>
class Room
{
int width;
int height;
static int copyConsCount;
public:
void Room( )
{
width = 12;
height = 8;
}
}
```