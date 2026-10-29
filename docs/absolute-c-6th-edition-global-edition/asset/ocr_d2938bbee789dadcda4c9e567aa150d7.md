The number of elements in a vector is called the size of the vector. The member function size can be used to determine how many elements are in a vector. For example, after the previously shown code is executed, sample.size() returns 3. You can write out all the elements currently in the vector sample as follows:

```
for (int i = 0; i < sample.size(); i++)
    cout << sample[i] << endl;
```

The function size returns a value of type unsigned int, not a value of type int. This returned value should be automatically converted to type int when it needs to be of type int, but some compilers may warn you that you are using an unsigned int where an int is required. If you want to be very safe, you can always apply a type cast to convert the returned unsigned int to an int, or in cases like this for loop, use a loop control variable of type unsigned int as follows:

```
for (unsigned int i = 0; i < sample.size(); i++)
    cout << sample[i] << endl;
```

A simple demonstration illustrating some basic vector techniques is given in Display 7.7.

There is a vector constructor that takes one integer argument and will initialize the number of positions given as the argument. For example, if you declare v as follows:

```
vector<int> v(10);
```

then the first ten elements are initialized to 0 and v.size() would return 10. You can then set the value of the i th element using v[i] for values of i equal to 0 through 9. In particular, the following could immediately follow the declaration:

```
for (unsigned int i = 0; i < 10; i++)
    v[i] = i;
```

To set the i th element for i greater than or equal to 10, you would use push_back.

# PITFALL: Using Square Brackets beyond the Vector Size

If v is a vector and i is greater than or equal to v.size(), then the element v[i] does not yet exist and needs to be created by using push_back to add elements up to and including position i. If you try to set v[i] for i greater than or equal to v.size(), as in

```
v[i] = n;
```

then you may or may not get an error message, but your program will undoubtedly misbehave at some point.