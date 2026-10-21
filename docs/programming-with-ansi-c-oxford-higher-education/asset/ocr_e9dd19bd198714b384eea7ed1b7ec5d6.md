# Note

It is by design that when an exception is thrown, the control gets permanently transferred to the catch block. Such behaviour looks very logical once we learn how real-world problems are solved. Take a case where a library designer develops a graphics library that is used by another user. Suppose the user sends a dimension to the graphics library and the dimensions are incorrect, then there is no point in executing the remaining statements and drawing that object further.

# How the Program Works

# Exceptions thrown

It should be noted that now the TestGen() function calls the ExGen() function. The exception thrown from ExGen() is caught in TestGen(), so it returns normally to main. Hence, the remaining single statement of main executes after the function call to TestGen() is over. It should also be noted that the remaining statements in TestGen() do not get executed.

# Separation of reporting from handling

Though Programs 8.2 and 8.3 looks similar to Program 8.1, there is a small change. Instead of throwing and catching the exception in the same function, they are done separately. Although it seems to be a simple change, it is big considering the separation of the error reporting and handling parts. Throwing now happens in ExGen() and catching happens in main and TestGen() in Programs 8.2 and 8.3, respectively.

# Inability of designer to provide appropriate messages

ExGen() can be used in various cases where exceptions are thrown. It is possible to write an appropriate error message in the catch statement for each such case in the program. Here, ExGen() is a very simple function and does almost nothing, but in real-life cases, it might do many actions to revert back to a stable state when a specific error occurs.

For example, assume that a globally available big array is present and that ExGen() is designed to allocate some memory in the array when the user asks for it. That portion of array may be used to store the information in the calling program. Understand that ExGen() is a common function for many objects and is used at different places by different objects for storing different types of objects. One may use ExGen() for storing Employee objects, another may use it to store the marks of students, and so on. Although the size of ExGen() array is big, it is not infinite and hence may run out of memory at some time. At that point, instead of providing space in the array, ExGen() throws an exception NotEnoughMemory.

Suppose ExGen() is used to allocate memory for the employee object in main where the exception NotEnoughMemory is caught, it is possible to display a message “Too many employee objects are created, cannot create any more”, which is easily understandable. Suppose an error message is provided in the ExGen() itself, then it would be similar to “No space left in the array”. ExGen() does not have any idea about the employee object, so it cannot be as precise as the main() function.

# Note

There are two reasons for ExGen() to have no knowledge about the employee array. The library designer has no idea about how that array will be used and which user will store what information in the array. Second, even when the user has an idea about the usage of the library, there is no method that can print a selective message for a specific usage. Take the case of using an aerospace design program and an architect using this library. When the out-of-dimension message is to be printed, what will the library designer prefer to print? In the given example, a user definitely prefers to have “Too many employee objects” rather than “No space left in the array”.

# Solution

Passing an exception is better in this case. The ExGen() function, instead of printing a message, passes the exception to the caller, which decides what to do with that exception, as it is definitely in a better position to print a more user-friendly message. In a