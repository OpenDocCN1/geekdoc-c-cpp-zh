but you also can’t remove properties or change their type (from data to accessor or vice versa). If an object is sealed, you can only read from and write to its properties.

You can use the Object.seal() method on an object to seal it. When that happens, the [[Extensible]] attribute is set to false, and all properties have their [[Configurable]] attribute set to false. You can check to see whether an object is sealed using Object.isSealed() as follows:

```
var person1 = {
  name: "Nicholas"
};

console.log(Object.isExtensible(person1)); // true
console.log(Object.isSealed(person1)); // false
```

+   ① Object.seal(person1);
+   ② console.log(Object.isExtensible(person1)); // false
+   console.log(Object.isSealed(person1)); // true
+   ③ person1.sayName = function() {
+     console.log(this.name);
+   };
+   console.log("sayName" in person1); // false
+   ④ person1.name = "Greg";
+   console.log(person1.name); // "Greg"
+   ⑤ delete person1.name;
+   console.log("name" in person1); // true
+   console.log(person1.name); // "Greg"
+   
+   var descriptor = Object.getOwnPropertyDescriptor(person1, "name");
+   console.log(descriptor.configurable); // false

This code seals person1 ① so you can’t add or remove properties. Since all sealed objects are nonextensible, Object.isExtensible() returns false ② when used on person1, and the attempt to add a method called sayName() ③ fails silently. Also, though person1.name is successfully changed to a new value ④, the attempt to delete ⑤ fails.

If you’re familiar with Java or C++, sealed objects should also be familiar. When you create a new object instance based on a class in one of those languages, you can’t add any new properties to that object. However, if a property contains an object, you can modify that object. In effect, sealed objects are JavaScript’s way of giving you the same measure of control without using classes.

**NOTE**

Be sure to use strict mode with sealed objects so you’ll get an error when someone tries to use the object incorrectly.