# Listing 13-2. Memory Allocation and Deallocation.

```
1 int main(void)
2 {
3 char *data2 = malloc(100);
4 NSString *myString = [[NSString alloc] init];
5 -- // standard "doing-stuff" ellipse
67 free(data2); // Deallocate the 100 bytes
8 data2 = NULL;
9 [myString release];
10 myString = nil;
11 }
```

In Listing 13-2, data2 is allocated on line 3. This type of allocation in Objective-C program is not typical in C and but it's still very important to know and understand.

Line 4 declares and allocates an Objective-C object, NSString.

Line 7 deallocates the block of memory allocated from line 3.

Line 8 sets the pointer to NULL. This is a good practice and will be explained in the next section.

Line 9 releases the object that was allocated on line 4. The release message is a request to deallocate the object. The reason release deallocate has to do with the mechanism of how memory is managed for Objective-C objects. This mechanism is referred to as the **retain/release model**, or sometimes as **counting**.

> Prior to Xcode 4, the retain/release model was the only model to use for iOS development. Xcode 4.2 introduced an option Automatic Reference Counting (ARC). ARC causes the compiler to automatically include the retain and release methods on your behalf. While ARC is optional, it defaults to being on any new project started in Xcode 4.2. Opening older projects created before Xcode 4.2 will still compile fine and ARC will be disabled.

While ARC is a nice feature, it's still very important to understand what is still happening under the covers. ARC doesn't remove calls to the retain and release methods, it just hides the implementation like Objective-C properties hide getter and setter methods.

Reference counting means making memory a little more efficient because it allows the objects to know when memory should be deallocated. It's a slightly better mechanism than completely managing memory manually.

Line 10 is equivalent to line 8. Objective-C pointers *can* be set to NULL and it's much better to set the pointer to nil. A *nil* object in Objective-C has a special meaning and can actually respond to a message. NULL does not have that property.

Let's also look at how this listing would change if we were to using ARC: