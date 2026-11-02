When used with the new operator, on the other hand, this type of function becomes an object constructor and effectively defines a class as we know in object-oriented programming. We can use it as follows:

```
```javascript
var fuzzyBunny = new Rabbit("cutie");
fuzzyBunny.speak("nibble, nibble!");
```
```

As Marijn points out, using new with a constructor function like this has a nice side effect that assigns the object's constructor property with the constructor function itself. This is not true if you just create a function that returns a newly instantiated object.

To make our class even more object-oriented, the other thing that we typically do is assign default values to properties and assign methods within the class, rather than on individual instances. In the first example above, each instance gets a new copy of the anonymous function assigned to speak. It would be better to define that function such that a single copy is used by the different instances of the class. This is accomplished by assigning the function to the class's prototype:

```
```javascript
function Rabbit(adjective) {
    this.adjective = adjective;
}
Rabbit.prototype.speak = function (line) {
    print("The " + this.adjective + " rabbit says '" + line + "'");
};
```
```

Of course, having to write this syntax out for each and every member of the class that's shared between instances is both cumbersome and prone to errors. Personally, I also like to avoid messing with prototype because you can really hurt yourself if you're not careful.

WinJS provides a helper that provides a cleaner syntax as well as clear separation between the constructor function, instance members, and static members: WinJS.Class.define:

```
```javascript
var ClassName = WinJS.Class.define(constructor, instanceMembers, staticMembers);
```
```

where constructor is a function and instanceMembers and staticMembers are both objects. The general structure you see in code looks like this (you can find many examples in the WinJS source code itself):

```
```javascript
var ClassName = WinJS.Class.define(
    function ClassName_ctor() { //adding _ctor is conventional
    },
    {
        //Instance members
    },
    {
        //Static members
    }
);
```
```

As many classes don't have static members, the third parameter is often omitted. Also, if you pass null as the constructor, WinJS will substitute an empty function in its place. You can see this in the WinJS source code for define (base.js, comments added):