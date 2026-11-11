For simplicity, we show the values pointed by the pointer directly within the object space in Figure 9.7 and later in this chapter. Remember, in actuality when a member is a pointer it stores address of a value which is actually present external to an object.

Recall from Chapter 8, Section 8.7, that creating a character pointer gives an additional flexibility of initializing it with string constant at any time in the program when compared to arrays. Hence we have created `title` and `author` as pointers rather than arrays.

![](bbox=[0.135, 0.218, 0.845, 0.32])

**Figure 9.8:** Storage of values for member `title`

Similarly, the members `id`, `author`, and `price` for each of the Book objects can be initialized by accessing the respective members for each of the objects by using a **membership operator ‘.’**

# Can we initialize all the members of the object in a single statement, instead of initializing one member at a time?

![](bbox=[0.148, 0.594, 0.191, 0.625])

Yes, we can initialize all the members of a particular object using a single statement. However, we can do so only at the time of creation of the object and no later than that. For example, we could have initialized the details of object `b1` at the time of creating it, using the following statement:

```
struct Book b1 = {1,"C++","Kunal",900};
```

The values defined in the curly brackets will be assigned to a particular member of the object in the same order in which they are declared inside the structure. This means that the id of object `b1` will be initialized as 1, the title will be initialized as "C++", author will be initialized as "Kunal" and the price will be initialized as 900. **The order in which the values are specified within the curly brackets must exactly match with the order in which the members are defined in the structure.**

I say it again, that such a initialization can only be applied at the time of creation of the object and not later than that. For example, the following code will not work because it first creates object `b1` and then initializes all its members in the second statement

```
struct Book b1; /*Create object b1*/
b1 = {1, "C++","Kunal", 900}; /*Error - cannot initialize object b1*/
```

If you need to initialize members of an object after its creation, you have to initialize them one at a time as shown below:

```
b1.id=1;
b1.title="C++";
b1.author="Kunal";
b1.price=900;
```