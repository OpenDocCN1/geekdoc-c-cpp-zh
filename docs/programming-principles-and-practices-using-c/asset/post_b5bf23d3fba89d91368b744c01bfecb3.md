
# Containers and Iterators

> “Write programs that do one thing
and do it well. Write programs
to work together.”
—Doug McIlroy

This chapter and the next present the STL, the containers and algorithms part of the C++ standard library. The STL is an extensible framework for dealing with data in a C++ program. After a first simple example, we present the general ideals and the fundamental concepts. We discuss iteration, linked-list manipulation, and STL containers. The key notions of sequence and iterator are used to tie containers (data) together with algorithms (processing). This chapter lays the groundwork for the general, efficient, and useful algorithms presented in the next chapter. As an example, it also presents a framework for text editing as a sample application.

### 20.1 Storing and processing data
#### 20.1.1 Working with data
#### 20.1.2 Generalizing code
### 20.2 STL ideals
### 20.3 Sequences and iterators
#### 20.3.1 Back to the example
### 20.4 Linked lists
#### 20.4.1 List operations
#### 20.4.2 Iteration
### 20.5 Generalizing vector yet again
#### 20.5.1 Container traversal
#### 20.5.2 *auto*
### 20.6 An example: a simple text editor
#### 20.6.1 Lines
#### 20.6.2 Iteration
### 20.7 vector, list, and string
#### 20.7.1 *insert* and *erase*
### 20.8 Adapting our vector to the STL
### 20.9 Adapting built-in arrays to the STL
### 20.10 Container overview
#### 20.10.1 Iterator categories

## 20.1 Storing and processing data

Before looking into dealing with larger collections of data items, let’s consider a simple example that points to ways of handling a large class of data-processing problems. Jack and Jill are each measuring vehicle speeds, which they record as floating-point values. Jack was brought up as a C programmer and stores his values in an array, whereas Jill stores hers in a **vector**. Now we’d like to use their data in our program. How might we do this?

We could have Jack’s and Jill’s programs write out the values to a file and then read them back into our program. That way, we are completely insulated from their choices of data structures and interfaces. Often, such isolation is a good idea, and if that’s what we decide to do we can use the techniques from Chapters 10–11 for input and a **vector<double>** for our calculations.

But, what if using files isn’t a good option for the task we want to do? Let’s say that the data-gathering code is designed to be invoked as a function call to deliver a new set of data every second. Once a second, we call Jack’s and Jill’s functions to deliver data for us to process:

```cpp
double* get_from_jack(int& count);  // Jack puts doubles into an array and
                                    // returns the number of elements in *count
vector<double> get_from_jill();      // Jill fills the vector

void fct()
{
    int jack_count = 0;
    double* jack_data = get_from_jack(&jack_count);
    vector<double>* jill_data = get_from_jill();
    // ... process ...
    delete[] jack_data;
    delete jill_data;
}
```

The assumption is that the data is stored on the free store and that we should delete it when we are finished using it. Another assumption is that we can’t rewrite Jack’s and Jill’s code, or wouldn’t want to.

### 20.1.1 Working with data

Clearly, this is a somewhat simplified example, but it is not dissimilar to a vast number of real-world problems. If we can handle this example elegantly, we can handle a huge number of common programming problems. The fundamental problem here is that we don’t control the way in which our “data suppliers” store the data they give us. It’s our job to either work with the data in the form in which we get it or to read it and store it the way we like better.

What do we want to do with that data? Sort it? Find the highest value? Find the average value? Find every value over 65? Compare Jill’s data with Jack’s? See how many readings there were? The possibilities are endless, and when writing a real program we will simply do the computation required. Here, we just want to do something to learn how to handle data and do computations involving lots of data. Let’s first do something really simple: find the element with the highest value in each data set. We can do that by inserting this code in place of the “… process …” comment in fct():

```cpp
// ...
double h = -1;
double* jack_high; // jack_high will point to the element with the highest value
double* jill_high;  // jill_high will point to the element with the highest value
for (int i=0; i<jack_count; ++i)
    if (h<jack_data[i]) {
        jack_high = &jack_data[i];     // save address of largest element
        h = jack_data[i];              // update "largest element"
    }

h = -1;
for (int i=0; i<jill_data->size(); ++i)
    if (h<(*jill_data)[i]) {
        jill_high = &(*jill_data)[i];  // save address of largest element
        h = (*jill_data)[i];           // update "largest element"
    }

cout << "Jill's max: " << *jill_high
     << "; Jack's max: " << *jack_high;

// ...
```

Note the ugly notation we use to access Jill’s data: `(*jill_data)[i]`. The function `get_from_jill()` returns a pointer to a `vector`, a `vector<double>*`. To get to the data, we first have to dereference the pointer to get to the `vector`, `*jill_data`, then we can subscript it. However, `*jill_data[i]` isn’t what we want; that means `*(jill_data[i])` because `[]` binds tighter than `*`, so we need the parentheses around `*jill_data` and get `(*jill_data)[i]`.

**TRY THIS**

If you were able to change Jill’s code, how would you redesign its interface to get rid of the ugliness?

### 20.1.2 Generalizing code

What we would like is a uniform way of accessing and manipulating data so that we don’t have to write our code differently each time we get data presented to us in a slightly different way. Let’s look at Jack’s and Jill’s code as examples of how we can make our code more abstract and uniform.

Obviously, what we do for Jack’s data strongly resembles what we do for Jill’s. However, there are some annoying differences: `jack_count` vs. `jill_data->size()` and `jack_data[i]` vs. `(*jill_data)[i]`. We could eliminate the latter difference by introducing a reference:

```cpp
vector<double>& v = *jill_data;
for (int i=0; i<v.size(); ++i)
    if (h<v[i]) {
        jill_high = &v[i];
        h = v[i];
    }
```

This is tantalizingly close to the code for Jack’s data. What would it take to write a function that could do the calculation for Jill’s data as well as for Jack’s? We can think of several ways (see exercise 3), but for reasons of generality which will become clear over the next two chapters, we chose a solution based on pointers:

```cpp
double* high(double* first, double* last)
// return a pointer to the element in [first,last) that has the highest value
{
    double h = -1;
    double* high;
    for(double* p = first; p!=last; ++p)
        if (h<=*p) { high = p; h = *p; }
    return high;
}
```

Given that, we can write

```cpp
double* jack_high = high(jack_data, jack_data+jack_count);
vector<double>& v = *jill_data;
double* jill_high = high(&v[0], &v[0]+v.size());
```

This looks better. We don’t introduce so many variables and we write the loop and the loop body only once (in high()). If we want to know the highest values, we can look at *jack_high and *jill_high. For example:

```cpp
cout << "Jill's max: " << *jill_high
     << "; Jack's max: " << *jack_high;
```

Note that high() relies on a vector storing its elements in an array, so that we can express our “find highest element” algorithm in terms of pointers into an array.

**TRY THIS**

![](img/e0ceba017429f80f5cf63e81a1e7ef4f_747_0.png)

> We left two potentially serious errors in this little program. One can cause a crash, and the other will give wrong answers if high() is used in many other programs where it might have been useful. The general techniques that we describe below will make them obvious and show how to systematically avoid them. For now, just find them and suggest remedies.

This high() function is limited in that it is a solution to a single specific problem:

- It works for arrays only. We rely on the elements of a vector being stored in an array, but there are many more ways of storing data, such as lists and maps (see §20.4 and §21.6.1).
- It can be used for vectors and arrays of doubles, but not for arrays or vectors with other element types, such as vector<double> and char[10].
- It finds the element with the highest value, but there are many more simple calculations that we want to do on such data.
