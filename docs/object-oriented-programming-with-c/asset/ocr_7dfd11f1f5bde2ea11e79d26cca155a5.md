```
```cpp
};    };    int main( )    {

city *cptr[10]; // array of 10 pointers to cities

int n = 1; int option;

do
{

cptr[n] = new city; // create new city

cptr[n]->getname( );

n++;

cout << “Do you want to enter one more name?\n”;

cout << “(Enter 1 for yes 0 for no):”;

cin >> option;

}
while(option);

cout << “\n\n”; for(int i=1; i<=n; i++) {

cptr[i]->printname( );

}

return 0;

}
```
```

The output of Program 9.9 would be: