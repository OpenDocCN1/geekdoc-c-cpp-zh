# Linked List Applications

Display 17.17 Interface File for a Stack Template Class

```
//This is the header file stack.h. This is the interface for the class
//Stack, which is a template class for a stack of items of type T.
#ifndef STACK_H
#define STACK_H
namespace StackSavitch {
    template<class T>
    class Node {
    public:
        Node(T theData, Node<T>* theLink) : theData(theData), link(theLink){
            Node<T>* getLink() const { return link; }
            T getData() const { return data; }
            void setData(const T& theData) { data = theData; }
            void setLink(Node<T>* pointer) { link = pointer; }
    private:
        T data;
        Node<T>* *link;
    };
    template<class T>
    class Stack {
    public:
        Stack();
        //Initializes the object to an empty stack.
        Stack(Stack<T>& other)& operator=(const Stack<T>& rightSide);
        virtual ~Stack();
        void push(T stackFrame);
        //Postcondition: stackFrame has been added to the stack.
        T pop();
        //Precondition: The stack is not empty.
        //Returns the top stack frame and removes that top
        //stack frame from the stack.
        bool isEmpty() const;
        //Returns true if the stack is empty. Returns false otherwise
    private:
        Node<T>* *top;
    };
}
#endif //STACK_H
```

You might prefer to replace the parameter T with const T&.

![](bbox=[0.673, 0.577, 0.792, 0.591])

> The destructor destroys the stack and returns all the memory to the freestore.