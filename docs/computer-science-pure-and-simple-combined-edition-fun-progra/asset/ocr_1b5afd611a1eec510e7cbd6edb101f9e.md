Our “Hello out there!” would look like this:

```
print [Hello out there!]
```

How do we get it to print out what's in (:) a variable? On the Procedures Page, let's try this:

```
to test
local :noun1
make "noun1" "me"
print [Hello :noun1]
```

Type test in the Command Center, and press Enter. Oops! It printed “Hello :noun1” in the box! That's not what we want! We want what's in noun1!

Let's look at a procedure called sentence. Here's what Help has to say about sentence:

```
sentence (se) word-or-list1 word-or-list2
(sentence word-or-list1 word-or-list2 word-or-list3...)
```

Reports a list which is made up of its inputs (words or lists). Sentence can take more than 2 inputs when sentence and the inputs are enclosed in parentheses. See list.

Examples:

```
show sentence "a "b
ab
show (sentence "hi "there [Bill]")nhi there Bill
```

This is telling us to use this format:

```
print (sentence input1 input2 input3)
```

Notice the parentheses that include the word sentence and all the inputs. Each of these inputs needs to be one of these:

+   1. a word, with a " mark
2. a list, using [brackets]
3. “what's in” a variable, for example :noun1

I want you to look at these commands, and guess which ones should work. Then test them in a test procedure. To make them work, first type this into the procedure:

```
to test
local [animal age] ;these are two variables
make "animal "cow
```