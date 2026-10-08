# 26 What's an int?

The first line means, "Carve off a small amount of storage in the computer's memory and assign it the name n." This step is analogous to reserving one of those lockers at the train station and slapping the label n on the side. The second line says, "Store the value 1 in the variable n, replacing whatever storage locker already contains." The train-locker equivalent is, "Open the train locker, rip out whatever happens to be in, and show a 1 in its place."

![](bbox=[0.14, 0.233, 0.228, 0.335])

The equals (=) is called the assignment operator.

The mathematician says, "n equals 1." The C# programmer says in a more precise way, "Store the value 1 in the variable n." (Think about the locker, and see why that's preferable.) C operators tell the computer what you want to do. In other words, operators are verbs and not descriptors. assignment operator takes the value on its right and stores it in the variable of. We leave a lot more operators in Chapter 3 of this minibook.

# What's an int?

In C#, each variable has a fixed type. When you allocate one of those lockers, you have to pick the size you need. If you pick an integer locker, for instance, you can't turn around and hope to stuff the entire state of Texas in it — Rhode Island, not Texas.

For the example in the preceding section of this chapter, you select a locker that's designed to hold an integer — C calls it an int. Integers are the counting numbers 1, 2, 3, and so on, plus the negative numbers -1, -2, -3, and so on.

![](bbox=[0.14, 0.638, 0.228, 0.695])

Before you use a variable, you must declare it. After you declare a variable as int, it can hold and regurgitate integer values, as this demonstrates:

```
// Declare a variable n - an empty train locker.
int n;
// Declare an int variable m and initialize it with the value 2.
int m = 2;
// Assign the value m to the variable n.
n = m;
```

The first line after the comment is a declaration that creates a little storage area, n, designed to hold an integer value. The initial value of n is not specified until it is assigned a value. The second declaration only declares an variable but also initializes it with a value of 2, all in one place.

![](bbox=[0.14, 0.888, 0.228, 0.94])

The term initialize means to assign an initial value. To initialize a variable is to assign it a value for the first time. You don't know for sure what the value of a variable is until it has been initialized. Nobody knows.