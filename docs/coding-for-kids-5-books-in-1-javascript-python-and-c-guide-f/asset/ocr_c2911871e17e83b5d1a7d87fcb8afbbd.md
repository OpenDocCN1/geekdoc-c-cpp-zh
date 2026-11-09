# # Arrays

An array in JavaScript is used to store a group of similar variables. Think about how you would store ages of people using variables. Let’s say we have three people and their ages. We can store them in variables age1; age2 and age 3.

```
```javascript
age1=5;
age2=25;
age=45;
```
```

Now, let’s say we have 10 people. We can store it in variables age1, age2….. age10. Now, what if we had to store it for 100 people. You get the picture. There are too many variables to track. For this reason, we use arrays. For storing 10 ages, we can just use.

```
```javascript
age=[5,25,45,60,20,23,24,43,34,78];
```
```

To access the values in Javascript, we use the index of the array. The index of the 1ˢᵗ element is 0, 2ⁿᵈ is 1, 3ʳᵈ is 2 and so on…… For example,

**document.write(age[0])** outputs 5;

**document.write(age[1])** outputs 25;

**document.write(age[5])** outputs 23.

# ## Example 1 – Creating An Array in JavaScript

Now, let’s look at the example below. We create 3 arrays in JavaScript for name, age and state of 5 people. We print these out using array index. And then we add a 6ᵗʰ person using **.push()** feature. Check out the code and output below.