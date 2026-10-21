```
```js
var person1 = new Person("Nicholas");
var person2 = new Person("Greg");
console.log(person1.name); // "Nicholas"
console.log(person1.getAge()); // 25
console.log(person2.name); // "Greg"
console.log(person2.getAge()); // 25
person1.growOlder();
console.log(person1); // Person { name: 'Nicholas', age: 26 }
console.log(person1.getAge()); // 26
console.log(person2.getAge()); // 26
```
```

In this code, the InnerPerson constructor ② is defined inside an IIFE. The variable age ① is defined outside the constructor but is used for two prototype methods. The InnerPerson constructor is then returned and becomes the Person constructor in the global scope. All instances of Person end up sharing the age variable, so changing the value with one instance automatically affects the other instance.

# # Mixins

Although pseudoclassical inheritance and prototypal inheritance are used frequently in JavaScript, there is also a type of pseudoinheritance accomplished through mixins. Mixins occur when one object acquires the properties of another object without modifying the prototype chain. The first object (a receiver) actually receives the properties of the second object (the supplier) by copying those properties directly. Traditionally, you create mixins using a function such as this:

```
```js
function mixin(receiver, supplier) {
  for (var property in supplier) {
    if (supplier.hasOwnProperty(property)) {
      receiver[property] = supplier[property]
    }
  }
  return receiver;
}
```
```

The mixin() function accepts two arguments: the receiver and the supplier. The goal of the function is to copy all enumerable properties from the supplier onto the receiver. You accomplish this using a for-in loop that iterates over the properties in supplier and then assigns the value