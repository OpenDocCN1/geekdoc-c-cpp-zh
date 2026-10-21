NOTE You can also explicitly call return inside of a constructor. If the returned value is an object, it will be returned instead of the newly created object instance. If the returned value is a primitive, the newly created object is used and the returned value is ignored.

Constructors allow you to initialize an instance of a type in a consistent way, performing all of the property setup that is necessary before the object can be used. For example, you could also use Object.defineProperty() inside of a constructor to help initialize the instance:

```
function Person(name) {

    Object.defineProperty(this, "name", {
        get: function() {
            return name;
        },
        set: function(newName) {
            name = newName;
        },
        enumerable: true,
        configurable: true
    });

    this.sayName = function() {
        console.log(this.name);
    };
}
```

In this version of the Person constructor, the name property is an accessor property that uses the name parameter for storing the actual name. This is possible because named parameters act like local variables. Make sure to always call constructors with new; otherwise, you risk changing the global object instead of the newly created object. Consider what happens in the following code:

```
var person1 = Person("Nicholas");        // note: missing "new"

console.log(person1 instanceof Person);    // false
console.log(typeof person1);                // "undefined"
console.log(name);                          // "Nicholas"
```

When Person is called as a function without new, the value of this inside of the constructor is equal to the global this object. The variable person1 doesn’t contain a value because the Person constructor relies on new to supply a return value. Without new, Person is just a function without a return statement. The assignment to this.name actually creates a global