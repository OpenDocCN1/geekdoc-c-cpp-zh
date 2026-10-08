
# 9.4 Introduction to Collections 425

## Adding and Inserting Elements

The Add and Insert methods add elements to the List (lines 17–18):

- The Add method appends its argument to the end of the List.
- The Insert method inserts a new element at the specified position.

Insert’s first argument is an index—as with arrays, collection indices start at zero. The second argument is the value to be inserted at the specified index. To make room for the new element, the indices of the elements at the specified index and above increase by one—in this case, "red" initially was at index 0, but now is at index 1, so that "yellow" can be inserted at 0.

## Count and Capacity

Lines 21–22 display the List’s Count (2) and Capacity (4) after the Add and Insert operations. When line 17 executes, the List grows, increasing its Capacity to 4 so that the List can accommodate four elements. One of these is immediately occupied by "red". At this point, the List’s Count is 1. When line 18 executes, there is still room for three more elements, so "yellow" is inserted and the Count becomes 2.

## Iterating through a List’s Contents

Lines 27–30 display the items in the List. Like array elements, List elements can be accessed by placing the index in square brackets after the List variable’s name. The Indexed List expression can be used to modify the element at the index. Lines 34–37 display the List using the preferred statement.

## Adding Elements and Growing the List

Lines 39–51 add more elements to the List, then display their Count, Capacity and contents once.

## Removing Elements

The Remove method deletes the first element with a specific value (line 53), returning true if successful and false otherwise. Lines 57–60 show the List’s contents after line 53 executes. A similar method, RemoveAt, removes the element at the specified index (line 62). When an element is removed through either of these methods, the indices of all elements above that decrease by one—the opposite of the Insert method. Lines 66–69 show the List’s contents after line 62 executes. Lines 72–73 display the List’s Count (2) and Capacity (4) after the remove operations. At this point, there’s room in the List for two more elements.

## Determining Whether an Element is in the List

Line 77 uses the Contains method to check whether an item is in the List. The Contains method returns true if the element is found in the List and false otherwise. The method compares its argument to each element of the List in order until the element is found, so using Contains on a large List is inefficient.

## Adding Elements and Growing the List

Lines 79–83 add more elements to the List. Before lines 78–80 execute, Count is 2 and Capacity is 4, so there’s room in the List for the two new elements added by those statements. When Line 81 executes, however, Count and Capacity are both 4, so the List doubles its Capacity to 8 and the Count becomes 5, leaving room for three more elements.

## Doubling the Capacity

When a List grows, it must (behind the scenes) create a larger internal array and copy each element to the new array. This is a time-consuming operation. It would be inefficient for the List to grow each time an element is added. To minimize of memory reallocations, a List doubles its capacity when more memory is required.

> Performance Tip 9.1
Doubling a List's Capacity is an efficient way for a List to grow quickly to the right size. This operation is more efficient than growing a List by only as much space as it takes to hold the element(s) being added. A disadvantage is that the List might occupy more space than it requires. This is a classic example of the spacetime trade-off.

> Performance Tip 9.2
It can be wasteful to double a List when more space is needed. For an example, a List of 1,000,000 elements resizes to 2,000,000 elements when one element is added. This wastes 999,999 elements. You can use Trim() to reduce a List's Capacity to its current Count. You can also set the Capacity to directly control space usage better—or if your List will never grow beyond 100 elements, you can preallocate that space by assigning 100 to the List's Capacity or using the List constructor that receives an initial capacity.

## 9.5 Querying the Generic List Collection using LINQ

As arrays, we use LINQ to Objects to query groups Lists. In Fig. 9.7, a List of strings is converted to objects and searched for those that begin with "R".

```
// Fig. 9.7: LINQWithListCollection.cs
// LINQ to Objects using a List<string>
using System;
using System.Linq;
using System.Collections.Generic;

class LINQWithListCollection
{
    static void Main()
    {
        var items = new List<string>();
        items.Add("Aqua"); // add "Aqua" to the end of the List
        items.Add("Rust"); // add "Rust" to the end of the List
        items.Add("Yellow"); // add "Yellow" to the end of the List
        items.Add("Red"); // add "Red" to the end of the List
```

(Note: The OCR text provided contained significant repetitive/interleaved sections in pages 426-428. Based on the flow of the document, the following sections represent the logical continuation of section 9.5.)

### 9.5.1 The let Clause

Line 30 uses LINQ's let clause to create a new variable. This is useful if you need to store a temporary result for later in the query. In this case, we use ToUpper to convert it to uppercase, then store it in the new variable. We then use uppercaseString in the where, select clauses. The clause (line 31) uses StartsWith performs a case-sensitive comparison to determine whether a string starts with the string received. If uppercaseString starts with "R", StartsWith returns true, and the element is in the query results.

### 9.5.2 Deferred Execution

We create the query once (lines 29–33), yet iterating over the results gives two different lists of-colors. This demonstrates LINQ query executes only when you access the results—like iterating over them or using the Count method—not when you define the query. This allows you to create a query once and execute it many times. Any changes to the data source are reflected in the results each time the query executes.

### 9.5.3 Extension Methods ToArray and ToList

There may be times when you want to retrieve a collection of the results immediately. LINQ provides extension methods ToArray and ToList for this purpose. These methods execute the query on they're called and give you the results as an array or List<T>, respectively.

### 9.5.4 Collection Initializers

Collection initializers provide a convenient syntax (similar to array initializers) for initializing a collection. For example, lines 12–16 of Fig.9.7 could be replaced with the following-statement:

```
var items = new List<string>{"Aqua", "Rust", "yElLow", "red"};
```
