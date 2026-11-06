The first three are the elements in `OrigList`, which we passed into the function: But they no longer have the values John, Paul, and George. The three original Beatles names have been replaced by three new names: Tom, Harry, and Suzy. However, the Copy variable still points to the original string list. Thus, once again, it worked.

We managed this change from John, Paul, and George to Tom, Suzy, and Harry by reference, but you can also do it with pointers. Here's the modified version of the function, this time using said pointers (as shown in the `Pointer04` example):

```
void ChangeAsPointer(StringArray *array)
{
    StringArray NameArray = new PChar[3];
    NameArray[0] = "Tom";
    NameArray[1] = "Harry";
    NameArray[2] = "Suzy";
    *array = NameArray;
}
```

As before, here’s the slightly modified sample code that tests the function:

```
StringArray OrigList = new PChar[3];
OrigList[0] = "John";
OrigList[1] = "Paul";
OrigList[2] = "George";
StringArray CopyList = OrigList;
ChangeAsPointer(CopyList);
cout << OrigList[0] << endl;
cout << OrigList[1] << endl;
cout << OrigList[2] << endl;
cout << CopyList[1] << endl;
cout << CopyList[2] << endl;
```

You can see that when we call `ChangeAsPointer()`, we’re passing the address of OrigList. The *output of this version is the same as that of the previous version.*

And now, as before, we unravel all this. Here are the two function headers without using the typedefs:

```
int ChangeAsReference(char **array) {
```

and

```
int ChangeAsPointer(char ***array) {
```