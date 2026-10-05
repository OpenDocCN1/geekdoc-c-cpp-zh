# Chapter 15

# Fine Tuning Objects

In Chapter 14 we introduced the basics of object-oriented programming: private data, public methods, and automatic initialization and destruction. In this chapter examine some details that enable C++ programmers to tune class design.

# 15.1 Pointers to Objects and Object Arrays

Given the Point class from Section 14.2, the statement

```
Point pt;
```

declares the variable pt to be a Point object. With primitive data, we can declare pointers to objects:

```
Point pt;
Point *p_pt;
```

Here, p_pt is a pointer to a Point object. Before we use the pointer we must initialize it to point to a valid object. We can assign the pointer to refer to an existing object, as in

```
p_pt = &pt;
```

or use the new operator to dynamically allocate an object from the heap:

```
p_pt = new Point;
```

If the class has a constructor that accepts parameters, we need to provide the appropriate arguments when using new. Recall the Account class from Section 14.4. The declarations

```
Account acc("Joe", 3143, 90.00);
Account *acct_ptr;
```

before we use acct_ptr must point to a valid object. As in the Point class example, we can assign the pointer to refer to an existing object, as in

```
acct_ptr = &acct;
```

or use the new operator to dynamically allocate an object from the heap: