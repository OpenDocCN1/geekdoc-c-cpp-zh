Although an adapter template class has a default container class on top of which it is built, you may choose to specify a different underlying container, for efficiency or other reasons, depending on your application. For example, any sequence container may serve as the underlying container for the stack template class, and any sequence container other than vector may serve as the underlying container for the queue template class. The default underlying data structure is the deque for both the stack and the queue. For a priority_queue, the default underlying container is a vector. If you are happy with the default underlying container type, then a container adapter looks like any other template container class to you. For example, the type name for the stack template class using the default underlying container is stack<int> for a stack of ints. If you wish to specify that the underlying container is instead the vector template class, you would use stack<int, vector<int>> as the type name. If you are using a version of C++ prior to C++11, then make sure to always insert a space between the two > symbols or the compiler will complain about a syntax error. This problem has been corrected starting with C++11 and a space is not needed.

The member functions and other details about the stack template class are given in Display 19.8. The details for the queue template class are given in Display 19.9. A simple example of using the stack template class is given in Display 19.10.

Warning!

# PITFALL: Underlying Containers

If you specify an underlying container, be warned that compilers prior to C++11 require an extra space between the last two > symbols, or your program will not compile. Use stack<int, vector<int> >, with a space between the last two > symbols. Do not use stack<int, vector<int>>. This problem has been corrected in C++11 and the space is not needed if you are using a C++11 compiler.

# Self-Test Exercises

+   11. What kind of iterators (forward, bidirectional, or random access) does the stack template adapter class have?
+   12. What kind of iterators (forward, bidirectional, or random access) does the queue template adapter class have?
+   13. If s is a stack<char>, what is the type of the returned value of s.pop()?