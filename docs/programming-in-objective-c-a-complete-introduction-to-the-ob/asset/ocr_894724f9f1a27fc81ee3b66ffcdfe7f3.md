# Note

Here the system is clever and determines that the immutable string object is initialized by a constant string object. Before the release of Leopard, this optimization was not done, and mystr2 would had a normal retain count.

# In the statement

```
NSMutableString *myStr3 = [NSMutableString stringWith:@string 3"];
```

the variable myStr3 is set to a string from a copy of the constant character string @string 3".A copy of the string had to be made because the message stringWith was sent to the NSMutableString class, indicating that the string's contents might have changed during the course of the program's execution. And constant character strings cannot have their contents, the system can't just get myStr3 variable to point to the constant string @string 3", as was done with myStr2.

So the object myStr3 has a meaningful reference count, as verified by the output. The return count can be changed by adding this string to an array or sending it a retain message, as verified by the output from the last calls NSLog. Foundation's stringWith: method added this object to the autorelease pool when it was created. Foundation's array method also added the array myArr to the pool.

Before the autorelease pool is released, myArr is released. The release of the autorelease pool decrements the reference count of this object to 0, which causes it to be deallocated. How does that happen? When each of the objects in the pool gets a release message sent to each time it was sent an autorelease message. Because the string object myStr3 was added to the autorelease pool when the stringWith: method created, it is sent to a release message. This brings its reference count down to 1.When an array in the autorelease pool is released, each of its elements is released. Therefore, when myArr is released from the pool, each of its elements—which includes myStr3—is sent release messages. This brings its reference count down to 0, which then causes it to be deallocated.

You must careful not to over-release an object. In Program 17.2, if you brought the reference count of mystr2 below 2 before the pool was released, the pool would end up with a reference to an invalid object. When the pool was released, the reference to the invalid object would most likely cause the program to terminate abnormally with a segmentation fault error.

# Instance Variables

You also pay attention to object references when you deal with instance variables. For example, recall the setName: method from your AddressClass:

+   - (void) setName:(NSString *)theName

```
{
if (name != theName) {
[name release];
name = [[NSString alloc] initWithString:theName];
}
```