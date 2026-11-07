```
DVD title (that is, the name of the movie)
movie star1
movie star2
movie producer
movie director
movie production co.
number of copiers
.
.
.
```

We will write a function, `createDVDList`, to read the data from the input file and create the list of DVDs. We will also write a function, `displayMenu`, to show the different choices—such as check in a movie or check out a movie—that the user can make. The algorithm of the function `main` is:

+   1. Open the input file.
+      If the input file does not exist, exit the program.
+   2. Create the list of DVDs (`createDVDList`).
+   3. Show the menu (`displayMenu`).
+   4. While not done
+      Perform various operations.

Opening the input file is straightforward. Let us describe Steps 2 and 3, which are accomplished by writing two separate functions: `createDVDList` and `displayMenu`.

# createDVDList

This function reads the data from the input file and creates a linked list of DVDs. Because the data will be read from a file and the input file was opened in the function `main`, we pass the input file pointer to this function. We also pass the DVD list pointer, declared in the function `main`, to this function. Both parameters are reference parameters. Next, we read the data for each DVD and then insert the DVD in the list. The general algorithm is:

+   a. Read the data and store it in a DVD object.
+   b. Insert the DVD in the list.
+   c. Repeat steps a and b for each DVD’s data in the file.

# displayMenu

This function informs the user what to do. It contains the following output statements:

Select one of the following:

+   1. To check whether the store carries a particular DVD
+   2. To check out a DVD