# Enumeration

By default, all properties that you add to an object are enumerable, which means that you can iterate over them using a for-in loop. Enumerable properties have their internal [[Enumerable]] attributes set to true. The for-in loop enumerates all enumerable properties on an object, assigning the property name to a variable. For example, the following loop outputs the property names and values of an object:

```
var property;

for (property in object) {
    console.log("Name: " + property);
    console.log("Value: " + object[property]);
}
```

Each time through the for-in loop, the property variable is filled with the next enumerable property on the object until all such properties have been used. At that point, the loop is finished and code execution continues. This example uses bracket notation to retrieve the value of the object property and output it to the console, which is one of the primary use cases for bracket notation in JavaScript.

If you just need a list of an object's properties to use later in your program, ECMAScript 5 introduced the Object.keys() method to retrieve an array of enumerable property names, as shown here:

```
var properties = Object.keys(object);

// if you want to mimic for-in behavior
var i, len;

for (i=0, len=properties.length; i < len; i++){
    console.log("Name: " + properties[i]);
    console.log("Value: " + object[properties[i]]);
}
```

This example uses Object.keys() to retrieve the enumerable properties from an object ①. A for loop is then used to iterate over the properties and output the name and value. Typically, you would use Object.keys() in situations where you want to operate on an array of property names and for-in when you don't need an array.

> NOTE There is a difference between the enumerable properties returned in a for-in loop and the ones returned by Object.keys(). The for-in loop also enumerates prototype properties, while Object.keys() returns only own (instance) properties. The differences between prototype and own properties are discussed in Chapter 4.