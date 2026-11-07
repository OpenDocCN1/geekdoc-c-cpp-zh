list of videos owned by the video store. The data in the input file is in the following form:

```
```
video title (that is, the name of the movie)
movie star1
movie star2
movie producer
movie director
movie production co.
number of copies
.
.
.
```
```

We will write a function, createVideoList, to read the data from the input file and create the list of videos. We will also write a function, displayMenu, to show the different choices—such as check in a movie or check out a movie—that the user can make. The algorithm of the function main is:

+   1. Open the input file.
+      If the input file does not exist, exit the program.
+   2. Create the list of videos (createVideoList).
+   3. Show the menu (displayMenu).
+   4. While not done
+      Perform various operations.

Opening the input file is straightforward. Let us describe Steps 2 and 3, which are accomplished by writing two separate functions: createVideoList and displayMenu.

**createVideoList** This function reads the data from the input file and creates a linked list of videos. Because the data will be read from a file and the input file was opened in the function main, we pass the input file pointer to this function. We also pass the video list pointer, declared in the function main, to this function. Both parameters are reference parameters. Next, we read the data for each video and then insert the video in the list. The general algorithm is:

+   a. Read the data and store it in a video object.
+   b. Insert the video in the list.
+   c. Repeat steps a and b for each video’s data in the file.

**displayMenu** This function informs the user what to do. It contains the following output statements:

Select one of the following:

+   1. To check whether the store carries a particular video
+   2. To check out a video