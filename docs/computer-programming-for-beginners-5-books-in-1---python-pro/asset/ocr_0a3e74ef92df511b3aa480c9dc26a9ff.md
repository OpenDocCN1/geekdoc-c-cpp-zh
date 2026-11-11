We have discussed different values such as Booleans, strings, and numbers whose values are difficult to change, although they can be combined to acquire new values from them. Objects are different from values, and it enables property changing; they can create different content for a single object value at different times. When there are two numbers, 120 and 120, they are considered the same, and there is a similarity between setting two references to one object and possessing two separate objects containing the same properties. Check the below code:

```
```javascript
let object1 = {value: 10};
let object2 = object1;
let object3 = {value: 10};
63
console.log(object1 == object2);
// → true
console.log(object1 == object3);
// → false
object1.value = 15;
console.log(object2.value);
// → 15
console.log(object3.value);
// → 10
```
```

The object1 and object2 bindings hold the same object, and that is why altering object1 one influences the value of object2. They are identical by nature. The binding object3 points to a separate object that consists of similar properties as the object1 but has a different life. Bindings can be constant or changeable, but it does not influence their values. A const binding an object cannot be transformed and relentlessly pointing to the same object. It is the object contents that can be changed.

```
```javascript
const score = {visitors: 0, home: 0};
// This is okay
score.visitors = 1;
// This isn't allowed
score = {visitors: 1, home: 1};
```
```

When the JavaScript’s == operator is used to differentiate objects, it uses the identity to perform that task. It will translate true if the objects contain the same value. Differentiating several objects will return false, even if their properties are similar.

# The lycanthrope's log