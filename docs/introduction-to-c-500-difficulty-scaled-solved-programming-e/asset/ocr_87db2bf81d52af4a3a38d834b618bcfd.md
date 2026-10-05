# Class Templates

In Chapter 16, we have discussed function templates. This chapter introduces you in the basics of class templates. You'll learn how to define and use class templates in your programs. Class templates are a powerful mechanism that allows us to define a class in a general way. Then, we can use the template to define specific versions of the class for different types of data. Both function and class templates are used extensively in the standard library to provide generic functions, algorithms, and data structures.

# CLASS TEMPLATES

Like function templates, class templates also provide the ability to program in a generic way. With class templates we can define generic purpose classes, that is, to which we can pass different types of data, without having to rewrite their code. For example, see again the implementation of the Lifo stack in exercise C.179. The type of elements stored in the stack is Node. If we want to store some other type (e.g., integers we have to replace all Node appearances with the new type and re-compile the program. That is, we cannot have two stacks in the same program, with Node elements and the other. We need to create a new stack (e.g., Lifo_Int), copy the code of the existing one and change the type from Node to int. If we want to create a new stack with another data type, we have to repeat this process.

To address this, C++ introduces the class templates so that we do not have to copy the code. An example of a class template is the vector class. We'll see more class templates in Chapter 26 when we discuss the standard template library. A class is defined in a generic way so that its operation does not depend on a particular type. The type of the elements each class object will work is passed as an argument to the generic parameters of the class. So, let's make the Lifo class, to see how more flexible the implementation becomes:

```
#include <iostream> // Example 23.1
#include <string>
#include <vector>
using std::cout;
using std::string;
using std::vector;
ntemplate <typename T> class Lifo
{
private:
    vector<T> vec_n;
public:
    void push(const T& t);
    void pop(T& t);
    void show_all() const;
    int get_nodes() const;
};
```