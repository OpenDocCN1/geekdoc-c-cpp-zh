# # 16

# # The string Class and the Standard Template Library

In this chapter you'll learn about the following:

+   - The standard C++ `string` class
+   - The `auto_ptr`, `unique_ptr`, and `shared_ptr` templates
+   - The Standard Template Library (STL)
+   - Container classes
+   - Iterators
+   - Function objects (functors)
+   - STL algorithms
+   - The `initializer_list` template

By now you are familiar with the C++ goal of reusable code. One of the big payoffs is when you can reuse code written by others. That's where class libraries come in. There are many commercially available C++ class libraries, and there are also libraries that come as part of the C++ package. For example, you've been using the input/output classes supported by the `ostream` header file. This chapter looks at other reusable code available for your programming pleasure.

You've already encountered the `string` class, and this chapter examines it more extensively. Then the chapter looks at "smart pointer" template classes that make managing dynamic memory a bit easier. Next, the chapter looks at the Standard Template Library (STL), a collection of useful templates for handling various kinds of container objects. The STL exemplifies the programming paradigm called *generic programming*. Finally, the chapter looks at the `initializer_list` template class, the C++11 addition that enables using initializer-list syntax with STL objects.