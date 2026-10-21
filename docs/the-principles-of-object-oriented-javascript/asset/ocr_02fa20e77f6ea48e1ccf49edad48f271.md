# IDENTIFYING A PROTOTYPE PROPERTY

You can determine whether a property is on the prototype by using a function such as:

```
function hasPrototypeProperty(object, name) {
  return name in object && !object.hasOwnProperty(name);
}
```

```
console.log(hasPrototypeProperty(book, "title")); // false
console.log(hasPrototypeProperty(book, "hasOwnProperty")); // true
```

If the property is in an object but hasOwnProperty() returns false, then the property is on the prototype.

# The [[Prototype]] Property

An instance keeps track of its prototype through an internal property called [[Prototype]]. This property is a pointer back to the prototype object that the instance is using. When you create a new object using new, the constructor's prototype property is assigned to the [[Prototype]] property of that new object. Figure 4-1 shows how the [[Prototype]] property lets multiple instances of an object type refer to the same prototype, which can reduce code duplication.

![](bbox=[0.32, 0.53, 0.88, 0.32])

> Figure 4-1: The [[Prototype]] properties for person1 and person2 point to the same prototype.