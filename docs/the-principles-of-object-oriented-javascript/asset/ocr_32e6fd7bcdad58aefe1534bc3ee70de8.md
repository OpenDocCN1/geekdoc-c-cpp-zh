The module pattern allows you to use regular variables as de facto object properties that aren’t exposed publicly. You accomplish this by creating closure functions as object methods. Closures are simply functions that access data outside their own scope. For example, whenever you access a global object in a function, such as window in a web browser, that function is accessing a variable outside its own scope. The difference with the module function is that the variables are declared within the IIFE, and a function that is also declared inside the IIFE accesses those variables. For example:

```
var person = (function() {
  ① var age = 25;
  return {
    name: "Nicholas",
    ② getAge: function() {
      return age;
    },
    ③ growOlder: function() {
      age++;
    }
  };
})();

console.log(person.name); // "Nicholas"
console.log(person.getAge()); // 25

person.age = 100;
console.log(person.getAge()); // 25

person.growOlder();
console.log(person.getAge()); // 26
```

This code creates the person object using the module pattern. The age variable ① acts like a private property for the object. It can’t be accessed directly from outside the object, but it can be used by the object methods. There are two privileged methods on the object: getAge() ②, which reads the value of the age variable, and growOlder() ③, which increments age. Both of these methods can access the variable age directly because it is defined in the outer function in which they are defined.