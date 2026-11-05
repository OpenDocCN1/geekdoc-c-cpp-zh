
Sounds like a genuine disadvantage, it isn't. At the point when you need a string that is a minor departure from one that already exists, just make another string that contains the desired changes. Since unused string objects are automatically garbage collected, you don't have to worry about what happens to the discarded strings.

It must be clarified, in any case, that string reference variables may, obviously, change which object they refer to. It is only that the contents of a particular string object can't be changed after it is created. To completely understand why immutable strings are not an obstacle, we will use another of string's methods: Substring(). The Substring() method returns another string that contains a predefined part of the invoking string. Since another string object is created that contains the substring, the first string is unaltered and the rule of immutability is still intact. The form of Substring() that we will use is shown here:

```
string Substring(int startIndex, int len)
```

Here, startIndex determines the starting index, and len indicates the length of the substring.

## Access Specifiers:

Member access control is accomplished using four access specifiers: public, private, protected, and internal. In this part we will be concerned about public and private. The protected modifier applies only when inheritance is involved, and is described later. The internal modifier applies generally to the use of an assembly, which in the case of C# means a program, project, or component. The internal modifier is briefly described later. When a member of a class is modified by the public specifier, that member can be accessed by any other code in your program. This includes methods defined inside other classes.

When a member of a class is specified as private, that member can be accessed only by other members of its class. Consequently, methods in other classes are not able to access a private member of another class. As explained in Chapter 4, if no access specifier is used, a class member is private to its class by default. Along these lines, the private specifier is optional when making private class members.

An access specifier precedes the rest of a member's type declaration. As should be obvious, inside the MyClass class, alpha is explicitly specified as private, beta is private by default, and gamma is specified as public. Since alpha and beta are private, they can't be accessed by code outside of their class. In this manner, inside the AccessDemo class, neither can be used directly. Each must be accessed through public methods, for example,

SetAlpha() and GetAlpha(). For instance, if you happen to remove the comment character from the start of the following line:

```
// ob.alpha = 10; // Wrong! alpha is private!
```

you would not be able to build this program because of the access violation. Although access to alpha by code outside of MyClass isn't permitted, methods defined inside MyClass can

openly access it, as the SetAlpha() and GetAlpha() methods appear. The same is valid for beta. The key point is this: A private member can be used freely by other members of its class, however, it can't be accessed by code outside its class.

To perceive how access control can be applied to an increasingly practical model, consider the following program that implements a "fail-soft" int array in which limit errors are avoided, thus avoiding a runtime exception. This is accomplished by encapsulating the array as a private member of a class, allowing access to the array only through member methods. With this approach, any attempt to access the array beyond its limits can be prevented, with such an attempt failing gracefully (thus resulting in a "soft" landing rather than a "crash"). The fail-soft array is implemented by the FailSoftArray class, shown here:

Let's take a look at this example. Inside FailSoftArray are defined three private members. The first is a, which stores a reference to the array that will really hold data. The second is errval, which is the value that will be returned

when a call to Get() fails. The third is the private method ok(), which decides whether an index is within limits. In this manner, these three members can be used only by other members of the FailSoftArray class. In particular, a and errval can be used only by other methods in the class, and ok() can be called only by other members of FailSoftArray. The remainder of the class members are public and can be called by any other code in a program that uses FailSoftArray.

When a FailSoftArray object is constructed, you should specify the size of the array and the value that you need to return if a call to Get() fails. The error value must be a value that would somehow not be stored in the array. Once constructed, the actual array referred to by a and the error value stored in errval can't be accessed by clients of the FailSoftArray object. Along these lines, they are not open to exploitation. For instance, the client can't attempt to index a directly, possibly exceeding its limits. Access is available only through the Get() and Put() methods.

The ok() method is private mainly for illustration. It is harmless to make it public since it doesn't alter the object. However, since it is used internally by the FailSoftArray class, it can be private. Notice that the Length instance variable is public. This is with regard to the way that C# implements arrays. To obtain the length of a FailSoftArray, simply use its Length member. To use a FailSoftArray array, call Put() to store a value at the specified index. Call Get() to retrieve a value from a specified index. If the index is outside the allocated boundaries, Put() returns false and Get() returns errval.

Since class members are private by default, there is no reason to explicitly declare them using private. Along these lines, from now on, this book won't repeatedly declare class members as private. Just remember that if a class member isn't preceded by an access modifier, its access is private.

You can use private access to make a somewhat significant improvement to the SimpleQueue class created in form, all members of the SimpleQueue class were

public. This implies it would be feasible for a program that uses a SimpleQueue to directly access the underlying array, possibly accessing its elements out of order. Since the whole purpose of a queue is to provide a first-in, first-out list, permitting out-of-order access isn't desirable. It would also be possible for a malicious programmer to modify the values stored in the putloc and getloc fields, thus undermining the queue. Luckily, these sorts of issues are simple to prevent by making portions of SimpleQueue private. As the previous example illustrated, passing an object reference to a method is a simple assignment. Nevertheless, there are a few subtleties that the example didn't show. In certain cases, the effects of passing an object reference will be different from those achieved when passing a value type. To perceive why, you have to understand the two ways in which an argument can be passed to a subroutine.

The first way is call-by-value. This method copies the value of an argument into the formal parameter of the subroutine. Consequently, changes made to the parameter of the subroutine have no effect on the argument. The second way an argument can be passed is call-by-reference. In this technique, a reference to an argument (not the value of the argument) is passed to the parameter. Inside the subroutine, this reference is used to access the actual argument specified in the call. This implies that changes made to the parameter will affect the argument used to call the subroutine.

Of course, C# uses call-by-value, which implies that a copy of the argument is made and given to the receiving parameter. Consequently, when you pass a value type, such as int or double, what happens to the parameter that receives the argument has no effect outside the method. As should be obvious, the actions that happen inside NoChange() have no effect on the values of a and b used in the call.

When you pass an object reference to a method, the situation is more complicated. In fact, the object reference itself is passed by value. Accordingly, a copy of the reference is made and changes to the parameter won't affect the argument. (For instance, making the parameter refer to another object won't change the object to which the argument refers.) However—and this is a
