You can provide any legal identifier you want for an array, programmers conventionally name arrays like they name variables—starting with a lowercase letter and using uppercase to begin subsequent words. Additionally, many programmers observe one of the following conventions to make it more obvious that the name represents a group of items:

+   - Arrays are often named using a plural noun such as sales.
- Arrays are often named by adding a final word that implies a group, such as salesList, salesTable, or salesArray.

After you declare an array variable, you still need to create the actual array because declaring an array and reserving memory space for it are two distinct processes. You can declare an array variable and reserve memory locations for 20 sales objects using the following statements:

```
double[] sales;
sales = new double[20];
```

The keyword is also known as the new operator; it is used to create objects. In this case, it creates 20 separate sales elements. You can also declare and create an array in one statement, such as following:

```
double[] sales = new double[20];
```

> You can change the size of an array associated with an identifier, if necessary. For example, if you declare int[] myArray; you can assign five elements later with myArray = new int[5]; later in the program, you might alter the array size to 100 with myArray = new int[100]; Most other programming languages do not provide this capability. You resize an array in C#, the same identifier refers to a new array in memory, and all values are set to the default value for the data type.

The statement double[] sales = new double[20]; reserves 20 memory locations. In C#, an array's elements are numbered beginning with 0, so if an array has 20 elements, you can use any subscript from 0 through 19. In other words, the first array element is sales[0], and the last element is sales[19].

Figure-6 shows how the array of 20 sales values appears in computer memory. The figure assumes that the array begins at memory address 20000. When you instantiate an array, you cannot choose its location in memory more than you can choose the location of any other variable. However, you know that after the first array element, the subsequent elements will follow immediately. Because a double takes eight bytes of storage, each element of a double array is stored in succession at an address that is eight bytes higher than the previous one.