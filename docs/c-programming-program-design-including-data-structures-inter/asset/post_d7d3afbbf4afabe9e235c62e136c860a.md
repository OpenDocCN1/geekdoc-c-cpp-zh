
- g. Overloads the operator `||`, as a member function, so that it returns true if two lines are parallel; false otherwise.
- h. Overloads the operator `&&`, as a member function, so that it returns true if two lines are perpendicular; false otherwise.

Write a program to test your class.

- 18. Consider the classes cashRegister and dispenserType given in the Programming Example “Juice Machine” in Chapter 10.
  - a. In the class cashRegister, add the functions to overload the binary operators + and − to add and subtract an amount in a cash register; the relational operators to compare the amount in two cash registers; and the stream insertion operator for easy output.
  - b. The class dispenserType, in the Programming Example “Juice Machine” in Chapter 10, is designed to implement a dispenser to hold and release products. In this class, add the functions to overload the increment and decrement operators to increment and decrement the number of items by one, respectively, and the stream insertion operator for easy output.
  - c. Write a program to test the classes designed in parts a and b.
- 19. **(Stock Market)** Write a program to help a local stock trading company automate its systems. The company invests only in the stock market. At the end of each trading day, the company would like to generate and post the listing of its stocks so that investors can see how their holdings performed that day. We assume that the company invests in, say, 10 different stocks. The desired output is to produce two listings, one sorted by stock symbol and another sorted by percent gain from highest to lowest.
  
  The input data is provided in a file in the following format:
  
  ```
  symbol openingPrice closingPrice todayHigh todayLow
  prevClose volume
  ```
  
  For example, the sample data is:
  
  ```
  MSMT 112.50 115.75 116.50 111.75 113.50 6723823
  CBA 67.50 75.50 78.75 67.50 65.75 378233
  .
  .
  .
  ```
  
  The first line indicates that the stock symbol is MSMT, today’s opening price was 112.50, the closing price was 115.75, today’s high price was 116.50, today’s low price was 111.75, yesterday’s closing price was 113.50, and the number of shares currently being held is 6723823.
  
  reads the data from the input file and stores it in the object `myStock`. (Note that this statement reads and stores the data in the relevant components of `myStock`).
  
  - b. Now that you have designed and implemented the class `stockType` to implement a stock object in a program, it is time to create a list of stock objects.
    
    Let us call the class to implement a list of stock objects `stockListType`.
    
    The class `stockListType` must be derived from the class `listType`, which you designed and implemented in the previous exercise. However, the class `stockListType` is a very specific class, designed to create a list of stock objects. Therefore, the class `stockListType` is no longer a template.
    
    Add a set of or overwrite the operations of the class `listType` to implement the necessary operations on a stock list.
    
    The following statement derives the class `stockListType` from the class `listType`.
    
    ```
    class stockListType: public listType<stockType>
    {
        member list
    };
    ```
    
    The member variables to hold the list elements, the length of the list, and the max listSize were declared as protected in the class `listType`. Therefore, these members can be directly accessed in the class `stockListType`.
    
    Because the company also requires you to produce the list ordered by the percent gain/loss, you need to sort the stock list by this component. However, you are not to physically sort the list by the component percent gain/loss. Instead, you will provide a logical ordering with respect to this component.
    
    To do so, add a member variable, an array, to hold the indices of the stock list ordered by the component percent gain/loss. Call this array `sortIndicesGainLoss`. When printing the list ordered by the component percent gain/loss, use the array `sortIndicesGainLoss` to print the list. The elements of the array `sortIndicesGainLoss` will tell which component of the stock list to print next.
  
  - c. Write a program that uses these two classes to automate the company’s analysis of stock data.
- 20. Write the definitions of the member functions of the classes `arrayListType` and `unorderedArrayListType`, which are not given in this chapter. Also, write a program to test your function.
- 21. Write the definition of the class template `orderedArrayListType`, derived from the class `arrayListType`, to implement an ordered list. As in Chapter 12, add the function `insert` in this class. Provide the definitions of the nonabstract functions. Also, write a program to test your class.
- 22. (Unordered Sets) Redo Programming Exercise 12 of Chapter 12 using templates.
- 23. (Ordered Sets) Redo Programming Exercise 13 of Chapter 12 using templates.

![](img/dc1b115c1ae2ec0d8a557b7c2b830e8c_1002_0.png)

## CHAPTER 14

## EXCEPTION HANDLING

### IN THIS CHAPTER, YOU WILL
- Learn what an exception is
- Learn how to handle exceptions within a program
- See how a try/catch block is used to handle exceptions
- Become familiar with C++ exception classes
- Learn how to create your own exception classes
- Discover how to throw and rethrow an exception
- Explore stack unwinding

An exception is an occurrence of an undesirable situation that can be detected during program execution. For example, division by zero is an exception. Similarly, trying to open an input file that does not exist is an exception, as is an array index that goes out of bounds.

Until now, we have dealt with certain exceptions by using either an if statement or the assert function. For instance, in Examples 5-3 and 5-4, before dividing sum by counter or count, we checked whether counter or count was nonzero. Similarly, in the Programming Example newString (Chapter 13), we used the assert function to determine whether the array index is within bounds.

On the other hand, there were places where we simply ignored the exception. For instance, while determining a substring in a string (Chapter 7), we never checked whether the starting position of the substring was within range. Also, we did not handle the array index out-of-bounds exception. However, in all of these cases, if exceptions occurred during program execution, either we included code to terminate the program or the program terminated with an appropriate error message. For instance, if we opened an input file in the function main and the input file did not exist, we terminated the function main, so the program was terminated.

There are situations when an exception occurs, but you don’t want the program to simply ignore the exception and terminate. For example, a program that monitors stock performance should not automatically sell if the account balance goes below a certain level. It should inform the stockholder and request an appropriate action. Similarly, a program that monitors a patient’s heartbeat cannot be terminated if the blood pressure goes very high. A program that monitors a satellite in space cannot be terminated if there is a temporary power failure on some section of the satellite.

The code to handle exceptions depends on the type of application you develop. One common way to provide exception-handling code is to add exception-handling code at the point where an error can occur. This technique allows the programmer reading the code to see the exception-handling code together with the actual code and to determine whether the error-checking code is properly implemented. The disadvantage of this approach is that the program can become cluttered with exception-handling code, which can make understanding and maintaining the program difficult. This can distract the programmer from ensuring that the program functions correctly.

### Handling Exceptions within a Program

In Chapter 3, we noted that if you try to input invalid data into a variable, the input stream enters the fail state, so an exception occurs. This occurs, for example, if you try to input a letter into an int variable. Chapter 3 also showed how to clear and restore the input stream. Chapter 4 introduced the assert function and explained how to use it to avoid certain unforeseeable errors, such as division by zero. Even though the function assert can check whether an expression meets the required condition(s), if the conditions are not met, it terminates the program. As indicated in the previous section, situations occur in which, if something goes wrong, the program should not be simply terminated.
