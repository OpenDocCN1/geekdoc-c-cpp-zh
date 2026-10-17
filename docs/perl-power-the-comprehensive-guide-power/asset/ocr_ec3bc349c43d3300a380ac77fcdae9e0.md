# CHAPTER 6  Array Fundamentals

```
```perl
@SomeArrayA = (@SomeArrayA, "Little");
@SomeArrayA = (@SomeArrayA, "things", "always");
@SomeArrayA = (@SomeArrayA, "matter", "in", "the", "end");
```
```

In each case, you assign the array back to itself as you populate it. No element is lost through the repeated list assignment operations.

With both the scalar and implicit (@) identifiers, when you assign values to arrays, you do not need to worry about data types. You can assign both numbers and strings. Certainly, in many respects, as with the creation of undefined value through arbitrary assignments, mixing array values can create problems. However, it remains that Perl arrays have no strict data types, so you can add whatever elements you want. Consider the following use of the list operator from Listing06_01:

```
```perl
@MixedArray = (32,all,22,44.7,32,34.5, numbers);
```
```

Each element is associated with an index. You can retrieve the value from the array using the index. The value the element possesses when you retrieve it from the array depends on how you use it. If you do not use the value in a specific way, it is displayed as a string value. Here are the values that display when you employ the print() function to print the interpolated elements:

```
```text
Mixed array: 32 all 22 44.7 32 34.5 numbers
```
```

# Retrieving and Printing Values

To retrieve a value using the scalar identifier, you employ the index of the value you want to retrieve. As shown in the lines associated with comment #2 in Listing06_01, you can concatenate it with an interpolated string or print it as a scalar value. For the item just assigned to index 1, you use the following statements:

```
```perl
print "$NL Array element identified by index 1: "
              $NewArray[1] . "$NL";

print "$NL Array element identified by index 1: $NewArray[1] $NL";
```
```

As Figure 6.2 illustrates, when the interpreter processes this statement, you see the following output for both statements:

```
```text
Array element identified by index 1: all
```
```

In a the previous list assignment, 32 was assigned to the 0 index. The word all was assigned to the 1 index. As you add them to your array, the values you add are assigned the next available index. To retrieve values for display, you can use the print() command and the index form of the array: