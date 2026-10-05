returned object foo on the stack is destroyed.

The destruction of this temporary object on the stack may cause unexpected side effects in some situations. For example, if the object returned by the function has a destructor that frees dynamically allocated memory, then this memory will be freed even though the object that is receiving the return value is going to use it.