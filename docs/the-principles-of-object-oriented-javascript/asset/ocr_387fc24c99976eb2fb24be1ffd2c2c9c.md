```
① Person.prototype.favorites = [];

var person1 = new Person("Nicholas");
var person2 = new Person("Greg");

person1.favorites.push("pizza");
person2.favorites.push("quinoa");

console.log(person1.favorites);    // "pizza,quinoa"
console.log(person2.favorites);    // "pizza,quinoa"
```

The favorites property ① is defined on the prototype, which means person1.favorites and person2.favorites point to the same array. Any values you add to either person's favorites will be elements in that array on the prototype. That may not be the behavior that you actually want, so it's important to be very careful about what you define on the prototype.

Even though you can add properties to the prototype one by one, many developers use a more succinct pattern that involves replacing the prototype with an object literal:

```
function Person(name) {
    this.name = name;
}

Person.prototype = {
    ① sayName: function() {
        console.log(this.name);
    },

    ② toString: function() {
        return "[Person " + this.name + "]";
    }
};
```

This code defines two methods on the prototype, sayName() ① and toString() ②. This pattern has become quite popular because it eliminates the need to type Person.prototype multiple times. There is, however, one side effect to be aware of:

```
var person1 = new Person("Nicholas");

console.log(person1 instanceof Person);      // true
console.log(person1.constructor === Person);  // false
① console.log(person1.constructor === Object);  // true
```