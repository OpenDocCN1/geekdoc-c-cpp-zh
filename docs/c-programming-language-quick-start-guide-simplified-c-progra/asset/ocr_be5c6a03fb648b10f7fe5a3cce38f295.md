The use of Functions give us many advantages such as reusability, modularity, readability, simplicity and maintainability.

The basic structuring element of C programs is Function. The standard C library itself, provides many built in functions such as sqrt, abs etc. We will see some of these functions in this chapter.

In C, we have two terminologies regarding Functions. One is Function-Declaration and the other one is Function Definition. Function Declaration means that the function is registered with compiler while Function Definition actually contains the body and functionality of the function.

# 5.1 Function Definition

The function definition is the actual code which is executed whenever that particular function is executed.

A function definition starts with the type of output a function provides. If no value is returned, then the type should be void. The default return type is int. If the type is other than void, then a value of that type is to be returned. If there is a mismatch between the