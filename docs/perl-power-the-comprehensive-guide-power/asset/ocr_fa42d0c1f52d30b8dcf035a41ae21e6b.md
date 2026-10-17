A similar procedure characterizes your use of the `values()` function. The `values()` function accesses all the values in a hash, and if you cascade the `values()` function into the `scalar()` function, you get a count of all the values in a hash.

For the two hashes representing the data used by Mendeleev and Newlands, you use the `scalar()` function and the cascaded `keys()` and `values()` functions to define four scalar identifiers ($MLenV, $MLenK, $NLenK, $NLenV). Having obtained these values, you can then proceed to print them. Figure 9.3 shows you the table that results from Listing09_03.

![](bbox=[0.12, 0.281, 0.655, 0.425])

**Figure 9.3**  
Use the `scalar()` function to retrieve the number of elements.

# Slicing Hashes

When you use a slice operation, you can insert the contents of one or more other hashes into a hash. You can improvise an endless number of approaches to hash slicing. The procedure usually involves the use of the lookup form of the target hash. You follow this with an assignment operation involving a list of items to be sliced into the target hash. In other cases, you can avoid using the lookup operation and employ instead assignment of a list alone. Listing09_04 presents three possibilities:

+   - Use the hash lookup operation with a series of keys separated by commas. Assign a list of values to the keys. See comment #4.
+   - Use the hash lookup operation. As the argument for the lookup, use `keys()` with the hash from which you want to derive keys for splicing. Follow with the assignment operator and a list containing the `values()` function. For the argument of the `values()` function, you use the same hash you used in the `keys()` function. See comment #5.
+   - Use the assignment operator to assign a list of hashes to the target hash. As the first item in the list, name the target list. See comment #6.

```
#Listing09_04
# 1 Formatting elements for the table
$NL = "\n ";
$DC = "=";            #character for top and bottom lines of table
```