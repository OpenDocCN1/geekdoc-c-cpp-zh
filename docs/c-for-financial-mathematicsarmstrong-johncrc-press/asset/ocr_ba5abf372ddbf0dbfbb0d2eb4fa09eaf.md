it should be implemented, what the return type should be, and whether or not it should be written as a member function. Consult a text such as [13] for details.

+   How to write a destructor for classes that manage memory and other resources. Note that most classes don’t need a destructor.

+   The rule of three: Whenever we write a destructor we write a copy constructor and override `=`.

Although we have implemented a sophisticated Matrix class in this chapter, we have done so purely to illustrate C++ techniques. Libraries containing much better Matrix implementations already exist.

# **Tip: Go easy on pointers and operator overloading**

+   Using pointers and operator overloading is justified for a Matrix class because we’ll use it so often.

+   Pointers are only really justified in our implementation for educational purposes. The code we’ve written would perform as well if we had used vector. If we had done this we would not have needed to write a destructor, copy constructor, or assignment operator.

+   Operator overloading is only justified because we come with expectations on how to add and multiply matrices. Don’t overload operators to give them strange meanings. This just makes code hard to read.

+   Realistically, a data structure such as a Matrix is the kind of class you should expect to find in a library rather than spending time writing it yourself.