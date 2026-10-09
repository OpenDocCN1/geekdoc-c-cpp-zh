```
string s("To be, or not to be?");
```

In the code above, **s** is an *object* of type **string**. It is an *instance* of the *class* **string**.

The term *object* in object-oriented programming refers to a data type which consists of a bundle of data together with helpful functions to work with that data.

So a **vector<double>** is an object because it contains the data of a vector and helpful functions like **size()**. Similarly a **string** is an object.

On the other hand, **double**, **int** and the raw data type **char*** are not object-oriented types because they consist purely of data with no special helper functions.

The type of data and functions supported by an object depend only on its *class*. All instances of the same class have the same functions and the same types of data.

**Example 2**: An instance of the class **string** consists of:

+   - data consisting of a sequence of characters;
- functions such as **size**, **insert**, **erase** for working with these data.

The *class* **string** is where all these functions and data types are defined.

Finally, the functions associated with an object are often called *methods*. There isn't meant to be any meaningful difference between the words *function* and *method*. Some authors prefer the word *method* as the word *function* can scare non-mathematicians. We will use both terms.

# 8.2 Writing your own class

# 8.2.1 Writing the declaration

To show how to write your own class, let us create a data type which represents a point in two-dimensional space.

```
class CartesianPoint {
public:
double x;
double y;
};
```