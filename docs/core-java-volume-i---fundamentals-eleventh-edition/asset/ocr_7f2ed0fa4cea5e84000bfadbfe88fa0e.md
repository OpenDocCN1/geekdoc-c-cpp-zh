Sometimes, you need to add elements in the middle of an array list. Use the add method with an index parameter:

```
```java
int n = staff.size() / 2;
staff.add(n, e);
```
```

The elements at locations n and above are shifted up to make room for the new entry. If the new size of the array list after the insertion exceeds the capacity, the array list reallocates its storage array.

Similarly, you can remove an element from the middle of an array list:

```
```java
Employee e = staff.remove(n);
```
```

The elements located above it are copied down, and the size of the array is reduced by one.

Inserting and removing elements is not terribly efficient. It is probably not worth worrying about for small array lists. But if you store many elements and frequently insert and remove in the middle of a collection, consider using a linked list instead. We explain how to program with linked lists in Chapter 9.

You can use the “for each” loop to traverse the contents of an array list:

```
```java
for (Employee e : staff)
    do something with e
```
```

This loop has the same effect as

```
```java
for (int i = 0; i < staff.size(); i++)
{
    Employee e = staff.get(i);
    do something with e
}
```
```

Listing 5.11 is a modification of the EmployeeTest program of Chapter 4. The Employee[] array is replaced by an ArrayList<Employee>. Note the following changes:

+   - You don’t have to specify the array size.
+   - You use `add` to add as many elements as you like.
+   - You use `size()` instead of length to count the number of elements.
+   - You use `a.get(i)` instead of `a[i]` to access an element.

```
```java
Listing 5.11  arrayList/ArrayListTest.java

1  package arrayList;
2
3  import java.util.*;
```
```

(Continues)