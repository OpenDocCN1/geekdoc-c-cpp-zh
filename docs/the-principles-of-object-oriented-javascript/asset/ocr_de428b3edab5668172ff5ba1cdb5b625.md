```
this.growOlder = function() {
    age++;
};
}

var person = new Person("Nicholas");

console.log(person.name);    // "Nicholas"
console.log(person.getAge());    // 25

person.age = 100;
console.log(person.getAge());    // 25

person.growOlder();
console.log(person.getAge());    // 26
```

In this code, the Person constructor has a local variable, age. That variable is used as part of the getAge() ① and growOlder() ② methods. When you create an instance of Person, that instance receives its own age variable, getAge() method, and growOlder() method. In many ways, this is similar to the module pattern, where the constructor creates a local scope and returns the this object. As discussed in Chapter 4, placing methods on an object instance is less efficient than doing so on the prototype, but this is the only approach possible when you want private, instance-specific data.

If you want private data to be shared across all instances (as if it were on the prototype), you can use a hybrid approach that looks like the module pattern but uses a constructor:

```
var Person = (function() {

    // everyone shares the same age
    var age = 25;

    function InnerPerson(name) {
        this.name = name;
    }

    InnerPerson.prototype.getAge = function() {
        return age;
    };

    InnerPerson.prototype.growOlder = function() {
        age++;
    };

    return InnerPerson;

})();
```