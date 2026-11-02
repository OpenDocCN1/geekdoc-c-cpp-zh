```
On_Call (Sunday) := False;

Total_Days := 0;
for Day in Day_Type loop
    if On_Call (Day) then
        Total_Days := Total_Days + 1;
    end if;
end loop;
```

Assignment is another operation available with arrays. As usual, strong typing requires that the source and target of an assignment statement be the same type. The following assignment statement makes the array Unknown a copy of the array Control.

```
Unknown := Control;
```

We can use the equality operators to compare two arrays of the same type. If the array components are discrete values, we can also compare two arrays with any of the relational operators. The relational operators are based on lexicographical order (sometimes called dictionary order) using the order relation of the discrete component type. We frequently use relational operators with arrays of characters (strings). Here is an example that uses two of the array variables we defined earlier:

```
if Control = Unknown then
    Put ("The values in the two arrays are identical");
elsif Control < Unknown then
    Put ("The values in Control come lexicographically before those in Unknown");
end if;
```

*Slicing* is another selection operation. It allows us to work with sub-arrays. We use slicing to read a portion of an array or write a portion of an array. A range is used to specify the portion of interest. Here are two examples of slicing:

+   - *Copy elements 11–20 into locations 1–10*
+     ```
+     Inventory (1 .. 10) := Inventory (11 .. 20);
+     ```
+   
+   - *Copy elements 2–11 into locations 1–10*
+     ```
+     Inventory (1 .. 10) := Inventory (2 .. 11);
+     ```

Our second example illustrates slice assignment with overlapping ranges. Such assignments are useful in shuffling the components in an array when inserting or deleting components in an array-based list.

Although indexing and slicing both access components, their results are quite different. The indexing operation accesses a single component. The