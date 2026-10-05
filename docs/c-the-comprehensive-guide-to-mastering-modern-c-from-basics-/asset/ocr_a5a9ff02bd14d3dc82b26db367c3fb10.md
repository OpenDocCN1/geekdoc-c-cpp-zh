```
std::cout << (bool)iptr << std::endl; // Output: 1 for
true
std::thread th2{showIptr, std::move(iptr)}; // Output: 657
std::this_thread::sleep_for(1s);
std::cout << (bool)iptr.get() << std::endl; // Output: 0 for
false
}
```

# **Listing 29.7** Using “move” to transfer inputs to the thread.

The Image class contains data representing a large actual image. I choose vector as the container for the data because it can be moved. And because I adhere to the rule of zero, the Image class is also movable.

Before start th1, image.data_ contains a lot of data. Due to std::move in the constructor of th1, the image or its content is moved into the thread. The local variable image in main is empty afterward, as indicated by the size 0.

It is similar with iptr, except that you cannot even copy a unique_ptr, even if you wanted to. Before creating th2, the pointer held by iptr is valid: (bool)iptr outputs 1, which stands for true. After moving at the start of th2, the same expression outputs 0 for false, which means that iptr no longer contains an int. It was moved into the thread function showIptr.

You do not need to keep jthread as a local variable. You can have a function or method create jthread instances—that is, return them as values.