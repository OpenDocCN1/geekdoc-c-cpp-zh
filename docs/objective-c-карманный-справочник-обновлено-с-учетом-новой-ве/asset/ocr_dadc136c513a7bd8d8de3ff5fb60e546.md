# Adding Methods to a Class 41

is referred to as a class extension. Unlike other categories, which should be accompanied by a separate @implementation directive specifying the category name, methods declared in class extensions are expected to appear in the main @implementation directive for the class. You can use this for forward-declaring private methods.

With the most recent Objective-C compilers, you may also declare instance variables inside class extensions. You can also declare instance variables inside @implementation contexts, just as you do inside @interface contexts. These two mechanisms allow you to move implementation details out of public headers.

If you are declaring private instance variables, then you should declare them in the @implementation context. This ensures that nothing that shouldn’t access them will do so by accident. If you are declaring public or protected instance variables that should only be accessed within the same library, then you should declare them in a class extension in a private header. In new code, you should only declare instance variables that are expected to be directly accessed by users of your code in public headers.