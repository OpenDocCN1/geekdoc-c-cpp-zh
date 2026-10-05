# Operator Overloading, Type Conversion, New Style Cases, RTTI 255

pointer is evaluated. During the first call to the new operator, its value will be NULL. Will soon see that its value will be NULL under a slightly circumstance also. The test expression in the if construct succeeds. Therefore, if if block executes. Sufficient memory for holding NO_OF_OBJECTS number of objects is allocated by calling the new operator. The address of this pool (in other words the address of the first object in this pool) is then stored in the temp pointer. After this, for the loop makes the value of the next pointer of each object (except the last object) in the newly created pool to the address of the next object. After the loop terminates, the last statement of the if block makes the next pointer of the last object NULL. With this, the if block terminates. The last statement of the function makes the head pointer to the second object of the pool. The value of temp, is, the address of the first object of the pool is returned by the new operator function. Thus, ClassNewPtr01 now points at the first object of the pool. ClassNewPtr01 now operates on the first object of the pool by calling the functions of that classNew.

Now let us at the fourth statement of the main function in Listing 8.48. The operator new function of classNew will be called for a second time. Again, temp pointer will be initialized to the current value of head which is not NULL (head is pointing at the second object of the pool). If if block will be executed. Only the last two statements execute. The head pointer is incremented to point at the next object (in this case the third) and the address of the object (in this case the second object) at which time is currently running.

This process will continue till operate the new function of the ClassNew is called for the fifth time (ClassNew * ClassNewPtr05 = new ClassNew). Although this is the test expression of the if block will, the value of the head pointer will be NULL while the address of the head and last object in the pool will be returned. Now, when the new operator is called for the sixth time, the test expression of if block succeeds. A fresh pool is allocated and the process repeats itself.

In order to make the operator new function succeed, it is necessary to free the memory using the for loop. This necessitates the presence of the next pointer in each object of the pool. Wastage of memory because of this next pointer, which would otherwise defeat the very purpose for which the new operator was overloaded, is easily prevented by the use of union.

Now let us see how we delete the delete operator for class ClassNew. The delete operator will be overloaded in a manner that will not deallocate the memory. Instead, the block at which, on whom the delete operator is applied points, will be put back in the free list. When the new operator is called for the next time, the address of that block will be returned. Before looking the actual code, let us see its effects.

Let us consider the case where the new operator is called only once. This solitary call is followed by a call to the delete operator (Listing 8.49).

# Listing 8.49 Calling an overloaded delete operator

```
/**ClassName NewDeleteForMemorySaveMain.cpp*/
#include<iostream>
#include"NewDeleteForMemorySave.h"
void main() {
    ClassNew* ClassNewPtr01 = new ClassNew;
    ClassNewPtr01->setx(10);

```