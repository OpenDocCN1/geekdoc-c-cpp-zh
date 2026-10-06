```
dataArray:
  one
  two
  three
dataArray2:
  one
  two
  three
```

You retrieved the first element of dataArray with the following
statement:

```
mStr = [dataArray objectAtIndexIndex: 0];
```

Then you appended the string @"ONE to it with this statement:

Notice the value of the first element of both the original array and its
copy: Both were modified. Perhaps you can understand why the first
element of dataArray was changed but not why its copy was
well. When you get an element from a collection, you get a new
reference to that element, but not a copy. So when the
objectAtIndex: method is invoked on dataArray, the returned
object points to the same object in memory as the first element in
dataArray. Subsequently modifying the string mStr has the
side effect of also changing the first element of dataArray, as you
see from the output.

But what about the copy you made? Why is its first element changed
as well? This has to do with the fact that copies, by default,
shallow copies. Thus, when the array was copied with the
mutableCopy method, space was allocated for a new object
in memory and the individual elements were copied into the new
array. But copying each element in the array from the original to a
new location meant just copying the reference from one element of