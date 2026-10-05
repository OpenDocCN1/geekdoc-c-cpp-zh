
```cpp
// https://godbolt.org/z/Y4sMdzde8
struct StereoImage {
    Image* right; // raw pointer
    Image* left; // raw pointer
    StereoImage(const string& nameBase) // construct
        : right{new Image(nameBase+"right.jpg")}, // okay
          left{new Image(nameBase+"left.jpg")} // dangerous
    {}
    ~StereoImage() { // remove
        delete right; delete left;
    }
    StereoImage(const StereoImage&) = delete; // no copy
    StereoImage& operator=(const StereoImage&) = delete; // no assignment
};

int main() {
    Image* image = new Image("image.jpg"); // a raw pointer?
    StereoImage stereo("3d");
    delete image;
}
```

**Listing 20.7** When a raw pointer owns an object, the potential errors are often hard to detect.

The raw image pointer stores the result of new. The corresponding delete is at the end of main. But what happens if this were another function in your program and an exception was thrown before delete? delete would never be executed, and you would have a memory leak. Always use smart pointers here:

- auto image = make_unique<Image>("image.jpg"); // also unique_ptr
- auto image = make_shared<Image>("image.jpg"); // also shared_ptr

Maybe you might say: "Then I'll just catch the exception and call delete afterward." Yes, that would be a start. But that won't save you during the initialization of links_: an exception in the constructor of Image during the initialization of links_ has very subtle effects. The new for right_ has already been executed and the memory requested. An exception during the initialization of left_ does prevent memory from being lost for left_, but right_ is retrievably lost. Because the exception leaves the constructor, stereo is considered not created—and thus the destructor with the delete statements is not called. You have no access to right_ to clean it up. You have a memory leak. [50]

I recommend using smart pointers here as well:

- unique_ptr<Image> right; unique_ptr<Image> left_; Or
- shared_ptr<Image> right; shared_ptr<Image> left_

And then initialize them with right{ new Image nameBase+"right.jpg" }, left_{ new Image nameBase+"left.jpg" } }. The problems are solved.

Another advantage is that you don't necessarily have to delete the copy constructor and assignment operator with = delete:

- With unique_ptr, these are impossible, and the compiler cannot generate them anyway—so you don't have to explicitly forbid them.
- With shared_ptr, you get both operations, and if you use them, they do what they are supposed to do and don't break your program.

You can read more about deleting methods in Chapter 16.

When raw pointers manage an object, they should not own it. However, to refer to an object that belongs to someone else, they are indeed very useful. You saw in Listing 20.1 using * in a container to modify the element in place. You have already encountered the & reference, a language element that allows you to refer to an element in the container. But that has not worked in the example. Because as practical and safe as a & reference is, it cannot do two things that a pointer can:

- **You cannot reassign a reference**
When you write int value = 42; int &ref = value; ref will always refer to value from now on. So with ref = 99; you are always assigning something to value. However, if you have an int *ptr = &value; pointer, you can achieve the same thing with *ptr = 66; as the reference, but you can point to a completely new variable. The following would not work with references:

```cpp
int value = 42;
int &ref = value;
ref = 99;                  // value is now 99
int *ptr = &value;         // value is now 66
*ptr = 66;
int new_value = 73;       // ptr no longer points to value
ptr = &new_value;
*ptr = -1;                // value remains 66, new_value is now -1
```

- **You cannot store references in a container**
There can be no vector<int>& or similar. A reference is something abstract that only exists for the compiler. In the compiled program and at runtime, you no longer see any trace of it. However, every container needs a physically present piece of memory for its elements. So here you need some form of pointer—be a smart pointer, raw pointer, or even iterator, as you will see later.

Here, raw pointers certainly have a field of application. If the objects in the container are not owned by the pointers, unique_ptrs are out of the question anyway. shared_ptrs would be possible, but why should you manage shared ownership when it does not? Raw pointers are just the right thing for that.

```cpp
// https://godbolt.org/z/W4W61h4Kv
#include <vector>
#include <numeric>    // iota
#include <iostream>

using std::vector; using std::cout;
struct Number {                // representative of a large, expensive object
    unsigned long val;
    Number(unsigned long val) : val{val} {}
    Number() : val{0} {}
};

/* determines whether z is a prime number */
bool isPrime(const Number& z, const vector<Number*>& primes) {
    for(Number* p : primes) { // iterate over
        if (p->val > z) return true; // greater than
        if (z % p->val == 0) return false; // divisor
    }
    return true; // found a new prime number
}

int main() {
    vector<Number> allNumbers(98); // 98
    std::iota(allNumbers.begin(), allNumbers.end(), 3); // from 3
    vector<Number*> primes; // result vector
    Number two{2}; // first prime number
    primes.push_back(&two); // store address
    for(Number &z : allNumbers) { 
        primes.push_back(&z); // append to
    }
    /* Output the rest */
    for(Number* p : primes) {
        cout << p->val << " ";
    }
    cout << "\n";
}
```
