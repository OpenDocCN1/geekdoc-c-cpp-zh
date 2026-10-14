Listing 7.2: Iterating through a list

```
```
>>> mylist = ["one", "two", "three"]
>>> for x in mylist:
...      print "number " + x
```

number one
number two
number three
```

In the above example, a list of text strings was created. Next, a simple *for* loop was used to iterate through the list, pre-pending the word "number" to each list object and printing them out. We will talk about *for* loops later but this is a common use of them.

One thing to note right now, however, is that you can use whatever value for "x" that you want, i.e. you can use whatever name you want instead of "x". I mention this because I kind of threw me for a loop when I first encountered it in Python. In other languages, loops like this are either hard-wired into the language and you have to use its format or you have to expressly create the "x" value beforehand so you can call it in the loop. Python's way is much easier because you can use whatever name makes the most sense, or you can simply use a "generic variable" like I did. For example, I could have used "for num in mylist:" or any other variation to iterate through the list. It's all up to you.

I won't go into the simple actions for lists since they work just like string operations. You can index, slice, and manipulate the list like you can for strings. In reality, a string is more like a modified list that only handles alphanumeric characters.

If you have questions, look at the chapter on Strings (Chapter 6); if you still have questions, look at the official Python documentation. Just remember that the resulting object will be a new list (surrounded by square brackets) and not a string, integers, etc.

# ## 7.2 Adding List Elements

Adding new items to a list is extremely easy. You simply tell the list to add it. Same thing with sorting a list.