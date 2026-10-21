# The this Object

You may have noticed something strange in the previous example. The sayName() method references person.name directly, which creates tight coupling between the method and the object. This is problematic for a number of reasons. First, if you change the variable name, you also need to remember to change the reference to that name in the method. Second, this sort of tight coupling makes it difficult to use the same function for different objects. Fortunately, JavaScript has a way around this issue.

Every scope in JavaScript has a this object that represents the calling object for the function. In the global scope, this represents the global object (window in web browsers). When a function is called while attached to an object, the value of this is equal to that object by default. So, instead of directly referencing an object inside a method, you can reference this instead. For example, you can rewrite the code from the previous example to use this:

```
var person = {
  name: "Nicholas",
  sayName: function() {
    console.log(this.name);
  }
};

person.sayName();      // outputs "Nicholas"
```

This code works the same as the earlier version, but this time, sayName() references this instead of person. That means you can easily change the name of the variable or even reuse the function on different objects.

```
function sayNameForAll() {
  console.log(this.name);
}

var person1 = {
  name: "Nicholas",
  sayName: sayNameForAll
};

var person2 = {
  name: "Greg",
  sayName: sayNameForAll
};

var name = "Michael";

person1.sayName();      // outputs "Nicholas"
person2.sayName();      // outputs "Greg"

sayNameForAll();        // outputs "Michael"
```