# Programming Projects 231

After you have completed the previous program, produce an enhanced version that also outputs a graph showing the average rainfall and the actual rainfall for each of the previous 12 months. The graph should be similar to the one shown in Display 5.4, except that there be two bars for each month and should be labeled as the average rainfall and the rainfall for the most recent month. Your program should ask the user whether he she wants to see the table or the bar graph, and display whichever format is requested. Include a loop that allows the user to select either format as the user wishes until requests the program end.

+   2. A write function deleteRepeats has a partially filled array of characters as a formal parameter and deletes repeated letters from the array. Since a partially filled array requires two arguments, the function will actually have two formal parameters: an array parameter and a formal parameter of type int that gives the number of array positions used. When a letter is deleted, the remaining letters are moved forward to fill in the gap. This will create empty positions at the end of the array so that less of the array is used. Since the formal parameter is a partially filled array, a second formal parameter of type int will tell how many array positions are filled. This second formal parameter will be a call-by-reference and change how much of the array is used after the repeated letters are deleted. For example, consider the following code:

```
char a[10];na[0] = 'a';
a[1] = 'b';
a[2] = 'c';
a[3] = 4;
deleteRepeats(a, size);
```

After this code is executed, the value of a[0] is 'a', the value of a[1] is 'b', the value of a[2] is 'c', and the value of size is 3. (The value of a[3] is no longer of concern, since the partially filled array no longer uses this indexed variable.) You may assume that the partially filled array contains only lowercase letters. Embed your function in a test test.

+   3. The standard deviation of a list of numbers is a measure of how much the numbers deviate from the average. If the standard deviation is small, the numbers are close to the average. The standard deviation, S, of a list of N numbers is defined as

```
S = \sqrt{rac{\sum_{i=1}^{N}(x_i-\bar{x})^2}{N}}$
```

where $\bar{x}$ is the average of the $N$ numbers $x_1, x_2, \dots$ Define a function that takes a partially filled array of numbers as its argument and returns the standard deviation of the numbers in the partially filled array. Since a partially filled array requires two arguments, the function will actually have two formal parameters: an array parameter