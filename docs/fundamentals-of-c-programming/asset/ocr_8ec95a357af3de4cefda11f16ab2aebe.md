```
SimpleRational one_third{1, 3};
auto other = zerol(one_third);
// Caller owns two objects: one_third (1/3) and other (0/3).
```

# 15.2 Pointers to Objects and Object Arrays

Given the Point class from Section 14.2, the statement

```
Point pt;
```

declares the variable pt to be a Point object. As with primitive data, we can declare pointers to objects:

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

If the class has a constructor that accepts parameters, we need to provide the appropriate arguments when using new. Recall the Account class from Section 14.4. Given the declarations

```
Account acct("Joe", 3143, 90.00);
Account *acct_ptr;
```

before we use acct_ptr it must point to a valid object. As in the Point class example, we can assign the pointer to refer to an existing object, as in

```
acct_ptr = &acct;
```

or use the new operator to dynamically allocate an object from the heap:

```
acct_ptr = new Account("Moe", 400, 1300.00);
```

Note that we include the arguments expected by the Account class constructor. This statement allocates memory for one Account object and executes the constructor's class code to initialize the newly created object. Figure 15.1 illustrates a pointer to an account object.

As with any dynamically allocated entity, a programmer must be careful to use the delete operator to deallocate any objects created via new.

The dot operator syntax to access a field of a object through a pointer is a bit awkward:

```
Point *p = new Point;
(*p).x = 253.7;
(*p).y = -00.5;
```

The parentheses are required since the dot (.) has higher precedence than the pointer dereferencing operator (*). Without the parentheses, the statement would be evaluated as if the parentheses were placed as shown here