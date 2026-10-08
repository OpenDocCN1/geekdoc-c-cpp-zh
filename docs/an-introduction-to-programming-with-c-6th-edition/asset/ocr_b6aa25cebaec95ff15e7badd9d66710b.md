# CHAPTER 11 One-Dimensional Arrays

attempt to compile the program. However, not all C++ compilers display a message when this error occurs. Rather, some compilers store the extra values in memory locations adjacent to, but not reserved for, the array. Therefore, you should be careful to provide no more than the appropriate number of `initialValues`.

# Entering Data into a One-Dimensional Array

As you can with a scalar variable, you can use either an assignment statement or the extraction operator to enter data into an array element. Figure 11-4 shows the syntax of such an assignment. In the syntax, `arrayName[subscript]` is the name and subscript of the array to which you want the `expression` assigned. The expression can include any combination of constants, variables, and operators. The data type of the `expression` must match the data type of array element to which is assigned; otherwise, an implicit conversion will occur, which could result in incorrect output. Also, Figure 11-5 shows examples of assignment statements that assign data to the elements in various arrays. The arrays were declared in Figure 11-3. The assignment statement in Example 1 assigns the letter Y to the second element in the `letters` array, replacing the letter B that was stored in the element when the array was declared. In Example 2 assigns the `double number` 0.0 to each of the elements in the `sales` array and provides another means of initializing the code. In Example 3 assigns the squares of the numbers from 1 through 6 to the six-element `numbers` array, replacing the initial values. The square of the number 1 is assigned to the `numbers[0]` element. The square of the number 2 is assigned to the `numbers[1]` element and so on. Notice that the x variable keeps track of the six numbers to be squared. Also notice that, in order to assign the square of each number to its appropriate element, the code must subtract the number 1 from the value stored in x variable. This is because the x's values go from 1 through 6, whereas their corresponding indices go from 0 to 5. Example 4's code updates the contents of each element in the six-element `numbers` array. It does this by adding the value contained in the `increase` variable to the value contained in the current array element and assigning the sum to the current array element. The loops in Examples 2 through 4 provide a convenient way to assign each element in a one-dimensional array.

> HOW TO Use an Assignment Statement to Assign Data to a One-Dimensional Array
arrayName[subscript] = expression;

Example 1
letters[1] = 'Y';
assign the letter Y to the second element in the letters array

Figure 11-4 How to use an assignment statement to assign data to a one-dimensional array (continues)

424