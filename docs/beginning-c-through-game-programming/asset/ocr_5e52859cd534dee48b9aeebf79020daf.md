# Concatenating string Objects

Next, I create a new string object, *phrase*, by concatenating the first three *string* objects:

```
string phrase = word1 + " " + word2 + word3;
```

As a result, *phrase* is "Game Over!!!".

Notice that the + operator, which you've seen work only with numbers, also concatenates *string* objects. That's because the + operator has been overloaded. Now, when you first hear the term *overloaded*, you might think it's a bad thing—the operator is about to blow! But it's a good thing. Operator overloading redefines a familiar operator so it works differently when used in a new, previously undefined context. In this case, I use the + operator not to add numbers, but to join *string* objects. I'm able to do this only because the *string* type specifically overloads the + operator and defines it so the operator means *string* object concatenation when used with strings.

# Using the size() Member Function

Okay, it's time to take a look at a *string* member function. Next, I use the member function *size()*:

```
cout << "The phrase has " << phrase.size() << " characters in it.\n\n";
```

*phrase.size()* calls the member function *size()* of the *string* object *phrase* through the member selection operator . (the dot). The *size()* member function simply returns an unsigned integer value of the size of the *string* object—its number of characters. Because the *string* object is "Lame Over!!!", the member function returns 12. (Every character counts, including spaces.) Of course, calling *size()* for another *string* object might return a different result based on the number of characters in the *string* object.

**Hint**

*string* objects also have a member function *length()*, which, just like *size()*, returns the number of characters in the *string* object.