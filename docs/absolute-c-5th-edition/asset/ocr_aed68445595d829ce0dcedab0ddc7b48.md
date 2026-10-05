# Display 16.10 Demonstration Program for Template Class PFArrayBak (part 2 of 2)

```
for (int i = 0; i < cap; i++)
{
    cin >> next;
    a.addElement(next);
}
int count = a.getNumberUsed() ;
cout << "The following " << count <<n" strings read and stored:\\n";
int index;
for (index = 0; index < count; index++) {
    cout << a[index] << " " ";
}
cout << "Backing up array.\\n";
a.backup();
cout << "Emptying array.\\n";
a.emptyArray();
cout << a.getNumberUsed ()
cout << " strings are now stored in the array.\\n";
a.restore();
count = a.getNumberUsed ()
cout << "The following " << count
 << " strings are now stored:\\n"
for (index = 0; index < count; index++) {
    cout << a[index] << " " ";
}
cout << endl;
cout << "End of demonstration.\\n";
return 0;
```

Sample Dialogue

| Enter capacity of this super array: 3 |
| Enter 3 strings |
| separated by you |
| I love you |
| The following 3 strings read and stored: |
| I love you |
| Backing up array. |
| Emptying array. |
| 0 strings are now stored in the array. |
| Restoring array. |
| The following 3 strings are now stored: |
| I love you |
| End of demonstration. |