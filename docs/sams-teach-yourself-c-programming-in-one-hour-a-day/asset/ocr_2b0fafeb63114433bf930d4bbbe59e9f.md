6. If you create a typedef called word, how would you declare a variable called
myWord using it?

7. Assume you have declared an array of structures and that ptr is a pointer to the
first array element (that is, the first structure in the array). How would you change
ptr to point to the second array element?

# # Exercises

+   1. Write code that defines a structure named time, which contains two int mem-
bers.

+   2. Write code that performs two tasks: defines a structure named data that contains
one type member and two float members, and declares an instance of
type data info.

+   3. Continuing with exercise 2, how would you assign the value 100 to the integer
member of the structure info?

+   4. Write code that defines and initializes a pointer to info.

+   5. Continuing with exercise 4, show two ways of using pointer notation to assign
value 5.5 to the first float member of info.

+   6. Write the definition for a structure type named data that can hold a single string of
u to 20 characters.

+   7. Create a structure containing five strings: address1, address2, city, state, and
zip. Create a typedef bool RECORD that can be used to create instances of
structure.

+   8. Using the typedef from exercise 7, allocate and initialize an element called
myaddress.

+   9. BUG BURSTER: What is wrong with the following code?

```
struct {
  char zodiac_sign[21];
  int month;
} sign = "Leo", 8;
```

+   10. BUG BURSTER: What is wrong with the following code?

```
/* setting up a union */
union data{
  char a_word[4];
  long a_number;
}generic_variable = { "WOW", 1000 };
```