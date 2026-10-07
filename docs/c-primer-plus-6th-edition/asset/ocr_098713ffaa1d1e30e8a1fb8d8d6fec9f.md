# Functions and Arrays

```
break;
} else if (temp < 0)   // signal to terminate
  break;
ar[i] = temp;
}
return i;
```

Note that this code includes a prompt to the user. If the user enters a non-negative value, the value is assigned to the array. Otherwise, the loop terminates. If the user enters only valid values, the loop terminates after it limits values. The last thing loop does is increment i, so after the loops,i is greater than the last array index, hence it's equal to the number of filled elements. The function that returns value.

# Showing the Array and Protecting it with const

Building a function to display the array contents is simple. You pass the name of the array and the number of filled elements to the function, which then uses a loop to display each element. But there is another consideration—guaranteeing that the display function doesn't alter the original. Unless the purpose of a function is to alter data passed to it, you should safeguard from doing so. Protection comes automatically with ordinary arguments because C++ passes them by value, and the functions that use an array work with the original. After all, that's the fill_array() function is able to do its job. To keep a function from accidentally altering the contents of an array argument, you can use the keyword const (discussed in Chapter 3,"Dealing with Data") when you declare the formal argument:

```
void show_array(const double ar[], int n);
```

The declaration states that the pointer points to constant data. This means that you can't use it to change the data. That is, you can use a value as ar [0], but you can't change value. Note that this doesn't mean the original array needs to be constant; it just means that you can't use ar in the show_array() function to change the data. Thus, show_array() treats the array as read-only data. Suppose you violate this restriction by doing something like the following in the show_array() function:

```
ar[0] += 10;
```

In this case, the compiler will put you to your wrongful ways. Borland C++, for example, gives an error message like this (edited slightly):

Cannot modify a const object in function

```
show_array(const double *,int);
```

Other compilers may choose to express their displeasure in different words.