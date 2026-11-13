```
```cpp
timetaken[2][1] = duration;
delete a;//assign 40000 to n
n = 40000;
input(n);
start = clock(); //time in milliseconds
heapsort(n);
finish=clock(); //time in milliseconds
duration = (double) ( (finish-start) ); //time in secs.
timetaken[3][1] = duration;
delete a;
```
```

```
```cpp
//assign 50000 to n
n = 50000;
input(n);
start = clock(); //time in milliseconds
heapsort(n);
finish=clock(); //time in milliseconds
duration = (double) ( (finish-start) ); //time in secs.
timetaken[4][1] = duration;
delete a;
```
```

```
```cpp
//quick sort
//assign 10000 to n
n = 10000;
input(n);
start = clock(); //time in milliseconds
quicksort(0,n-1);
finish=clock(); //time in milliseconds
duration = (double) ( (finish-start) ); //time in secs.
timetaken[0][2] = duration;
delete a;
```
```

```
```cpp
//assign 20000 to n
n = 20000;
input(n);
start = clock(); //time in milliseconds
quicksort(0,n-1);
finish=clock(); //time in milliseconds
duration = (double) ( (finish-start) ); //time in secs.
timetaken[1][2] = duration;
delete a;
```
```

```
```cpp
//assign 30000 to n
n = 30000;
input(n);
start = clock(); //time in milliseconds
quicksort(0,n-1);
finish=clock(); //time in milliseconds
duration = (double) ( (finish-start) ); //time in secs.
timetaken[2][2] = duration;
delete a;
```
```