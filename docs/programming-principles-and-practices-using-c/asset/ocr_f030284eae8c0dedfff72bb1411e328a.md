20.1 **Storing and processing data**  
20.1.1 Working with data  
20.1.2 Generalizing code  
20.2 **STL ideals**  
20.3 **Sequences and iterators**  
20.3.1 Back to the example  
20.4 **Linked lists**  
20.4.1 List operations  
20.4.2 Iteration  
20.5 **Generalizing vector yet again**  
20.5.1 Container traversal  
20.5.2 *auto**

20.6 **An example: a simple text editor**  
20.6.1 Lines  
20.6.2 Iteration  
20.7 **vector, list, and string**  
20.7.1 *insert* and *erase**  
20.8 **Adapting our vector to the STL**  
20.9 **Adapting built-in arrays to the STL**  
20.10 **Container overview**  
20.10.1 Iterator categories

# # 20.1 Storing and processing data

Before looking into dealing with larger collections of data items, let’s consider a simple example that points to ways of handling a large class of data-processing problems. Jack and Jill are each measuring vehicle speeds, which they record as floating-point values. Jack was brought up as a C programmer and stores his values in an array, whereas Jill stores hers in a **vector**. Now we’d like to use their data in our program. How might we do this?

We could have Jack’s and Jill’s programs write out the values to a file and then read them back into our program. That way, we are completely insulated from their choices of data structures and interfaces. Often, such isolation is a good idea, and if that’s what we decide to do we can use the techniques from Chapters 10–11 for input and a **vector<double>** for our calculations.

But, what if using files isn’t a good option for the task we want to do? Let’s say that the data-gathering code is designed to be invoked as a function call to deliver a new set of data every second. Once a second, we call Jack’s and Jill’s functions to deliver data for us to process:

```
```
double* get_from_jack(int& count);  // Jack puts doubles into an array and
                                     //  returns the number of elements in *count
vector<double> get_from_jill();      // Jill fills the vector

void fct()
{
    int jack_count = 0;
    double* jack_data = get_from_jack(&jack_count);
```

```