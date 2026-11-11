# Chapter 5: Data Structures: Objects and Arrays

Data layouts develop from Booleans, strings, and numbers fragments. Several types of information use more than one chunk. Objects enable the user to collate values together with other objects to develop more compound layouts. In this chapter, you will understand the concepts of solving a real problem at hand.

# Data sets

If you want to work with a lot of digital data, you must represent the digital data in the machine memory. For instance, you need to represent a group of numbers like 2, 3, 5, 7, and 11. Now let’s get prolific with our use of strings as strings can contain quite a lot of data. We will use 2 3 5 7 11 as the representation. JavaScript programming language offers a unique data type for saving sequences of values, which is called an array. Write an array as a list of values within the between square brackets, differentiated by commas.

```
let listOfNumbers = [2, 3, 5, 7, 11];
console.log(listOfNumbers[2]);
// → 5
console.log(listOfNumbers[0]);
// → 2
console.log(listOfNumbers[2 - 1]);
// → 3
```

The notation used to get elements within an array also utilize the square brackets. A complete square brackets pair right after an expression that contains another expression within. When you start counting elements in an array, you begin from zero and not one. Therefore the first element is redeemed with listOfNumbers[0].

# Properties

The previous chapters have contained expressions like the myString. Length (to calculate the length of a string) and Math.max (the maximum function). These are properties that can approach the property values. Virtually all JavaScript values contain properties. The few values that do not contain properties are null and undefined. If you access a property with a nonvalue, the result will be an error.

```
null.length;
// → TypeError: null has no properties
```

In JavaScript, the two major ways to evaluate properties are with a dot and square brackets. The value.x and value[x] can evaluate the property on value, not particularly the same property. How you use x is different from how you use a dot.

If you want to use the dot, the text you input after the dot is the name of the