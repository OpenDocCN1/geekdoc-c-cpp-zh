# 4.1. **AN INTRODUCTION TO ARRAYS**

In the previous sessions you have come across various methods of storing a particular number or character in the memory using variables. To accomplish this feat, a variable was needed and if 4 numbers were used, 4 variables were used. Now if you have to store 10 numbers? Quite possible one might say, but if 134 numbers have to be stored and retrieved whenever obligatory, is it still possible?

With arrays, it is. You may ask why didn’t you start with arrays in the first place? You needed to have some fundamental understanding of data types and their behavior in order to learn arrays. Moreover the concept of arrays depends on other data types, which was meant to facilitate the storage of copious amount of numbers in a single variable. One cannot imagine creating an array for a single number and wasting an entire consignment of space in the memory. It would be like buying a dozen books and ultimately using only one and dumping the rest in the garbage.

Thus arrays can be defined as a collection of similar elements. In your context an array of elements can be formed only if all the elements are of one particular data type, i.e., all of them are either integer or character or a floating point number, but there cannot exist an array which hosts an amalgamation of these data types.

# 4.2. **ADVANTAGES OF ARRAYS**

The usage of arrays is crucial to any professional programming. Arrays just make the life of a programmer a bit easier. Prima facie, it relieves him of the burden of having to keep naming the variables. They simply follow the good old slotted rack principle. An array is a single variable holding multiple data. Each data is referred to by its slot number. If for instance, you wish to store a list of items, you could just name the variable ‘item,’ and keep storing the data by referring to item(1), item(2), item(3), etc. It may sound pretty simple but the magnitude of work that can be accomplished using arrays is praiseworthy.

To gain a better insight into the advantages of arrays consider a simple example:

```
```c
main()
{
    int a, a=2; a=4;
}
```
```