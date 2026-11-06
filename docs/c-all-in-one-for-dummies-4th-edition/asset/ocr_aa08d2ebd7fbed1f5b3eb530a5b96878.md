```
```
MyFile.close();
return 0;
}
```
```

Each of the variables holds just one string element. To read all four numbers, you need to extract the data four times. The input file, Numbers.txt, has its numbers separated with spaces. You can also separate them with newline characters, like this:

```
```
100
50
30
25
```
```

The application doesn't care. It looks for white space, which is any number of spaces, tabs, and newlines. You could format the data so it looks like the following example, and the application will still read them in correctly.

```
```
100    50
       30
   25
```
```

![](bbox=[0.171, 0.516, 0.233, 0.584])

When you are dealing with the standard input object, `cin`, the same rules about white space apply: If you read in four numbers, as in the following example, the `cin` object, like the `ifstream` object, will separate the numbers based on the white space.

![](bbox=[0.171, 0.609, 0.233, 0.676])

Users make common mistakes that can cause your application to fail or possibly display incorrect information:

+   - If the user accidentally inserts a space into the input stream, whether from the console or a file, the computer sees the space as the beginning of a new string.
+   - Sometimes users forget to add white space, which means that two values mash together and the computer sees them as a single entity.
+   - A user might try to separate values using commas, semi-colons, or other non-white-space characters.
+   - Missing values, where the user simply leaves the data out, is also a problem.

Consequently, when you encounter problems with the input data, looking for additional white space, missing white space, or missing values is a good place to begin.