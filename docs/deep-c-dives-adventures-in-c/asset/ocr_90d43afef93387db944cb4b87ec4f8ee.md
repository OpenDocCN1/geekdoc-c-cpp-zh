As myArray is a pointer to any array of 6 ints, dereferencing it gives the array of 6 ints, which is, of course, a pointer to int. So:

* (myArray+1)

is a pointer to int, i.e. it is a one-dimensional array.

Thus:

*(* (myArray+i)+j)

is the jth element in the ith row.

Notice that all this works because the type of myArray is int (* ) [6] as this specifies how much to add in pointer arithmetic to move on to the next row. Also, even though this is a pointer to a pointer, there is no other pointer actually involved. There is only myArray pointing to the start of the entire array. The trick is all based on changing the type of the pointer to generate different pointer arithmetic so as to implement the storage mapping function needed for the dimension of the array. That is, myArray is of type int (* ) [6], so myArray+i implements myArray+i*6*sizeof(int) and *myArray is of type int [6] and so (*myArray)+j implements myArray+j*sizeof(int), which, when you put these together as *(*(myArray+i)+j), implements:

myArray +i*6*sizeof(int) +j*sizeof(int)

which is the SMF for the two-dimensional array.

This idea works no matter how many dimensions that array has. If the array is three-dimensional:

int myArray[2][3][4]

then myArray is of type int(* ) [3][4], i.e. an array of three elements each of which is an array of four ints. When you add one to myArray pointer arithmetic moves it on by three by four ints. Next we have *myArray which is of type int(* ) [4], i.e. an array of four ints. Adding one to this moves the pointer on by four ints and finally **myArray is simply a pointer to an int array. Thus to access the element given by i, j, k we use:

*(*(* (myArray+i)+j)+k)

It is difficult to follow the details, but it works as advertised.

Finally, notice that you can get a simple pointer to the start of the entire array using:

int *myPointer=(int *) myArray;

Using this you can implement your own SMF or access the array as a single dimension. It is a general principle that you get a pointer to the start of the array whenever you convert the array to a pointer.

127