a. (Stock Object) Design and implement the stock object. Call the class that captures the various characteristics of a stock object stockType.

The main components of a stock are the stock symbol, stock price, and number of shares. Moreover, we need to output the opening price, closing price, high price, low price, previous price, and the percent gain/loss for the day. These are also all the characteristics of a stock. Therefore, the stock object should store all this information.

+   Perform the following operations on each stock object:
+   
+    i. Set the stock information.
+    ii. Print the stock information.
+    iii. Show the different prices.
+    iv. Calculate and print the percent gain/loss.
+    v. Show the number of shares.

+   a.1. The natural ordering of the stock list is by stock symbol. Overload the relational operators to compare two stock objects by their symbols.
+   
+   a.2. Overload the insertion operator, <<, for easy output.
+   
+   a.3. Because the data is stored in a file, overload the stream extraction operator, >>, for easy input.

For example, suppose infile is an ifstream object and the input file was opened using the object infile. Further suppose that myStock is a stock object. Then, the statement:

```
infile >> myStock;
```

reads the data from the input file and stores it in the object myStock. (Note that this statement reads and stores the data in the relevant components of myStock.)

b. Now that you have designed and implemented the class stockType to implement a stock object in a program, it is time to create a list of stock objects.

Let us call the class to implement a list of stock objects stockListType.

The class stockListType must be derived from the class listType, which you designed and implemented in the previous exercise. However, the class stockListType is a very specific class, designed to create a list of stock objects. Therefore, class stockListType is no longer a template.

Add and/or overwrite the operations of the class listType to implement the necessary operations on a stock list.