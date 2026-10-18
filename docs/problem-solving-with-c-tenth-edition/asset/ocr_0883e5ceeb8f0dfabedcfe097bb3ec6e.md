Project 8 asked you to write a program to find all permutations of a set. Modify the program so that it generates permutations given an instance of the template-based set class defined in Programming Project 7. You may wish to also use your template-based set class to help simplify the implementation of the permutation algorithm itself.

The algorithm requires that you store a set of lists. C++ allows you to create a set of lists with your template-based set class. For example, `mySet<vector<T> >` will define a set containing a vector of type T. Be careful to place a space between the last two >’s, or the compiler may get confused. The code `mySet<vector<T>>` without a space will likely produce a compiler error unless you are using C++11 or higher.

Your program should print all permutations of sets of several different sizes and comprised of several different types of data (for example, a set of three integers, a set of four strings, or a set of five doubles).

+   9. In this chapter we used only a single template class type parameter. C++ allows you to specify multiple type parameters. For example, the following code specifies that the class accepts two type parameters:

```
template<class T, class V>
class Example
{
    ...
}
```

When creating an instance of the class, we must now specify two data types, such as:

```
Example<int, char> demo;
```

Create a Map class that maps keys to values. The data type for the keys and values should be specified separately using type parameters. The map forms the basis for a simple database. For example, to map from employee ID numbers to employee names, we might use integers for the data type of the keys and strings for the data type of the names. The class should have functions to:

+   1. Add a new key/value pair to the map
+   2. Set an existing key/value pair to a new value given the key
+   3. Delete a key/value pair from the map given the key
+   4. Check if a key/value pair exists in the map given the key
+   5. Retrieve the value for a key/value pair given the key

Use any data type you wish to implement the map. Write a main function that tests the class by exercising all of the functions with sample data.