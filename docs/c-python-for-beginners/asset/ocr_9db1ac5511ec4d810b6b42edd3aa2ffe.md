# # Conditions and Loops

Conditions and loops are what makes a program interesting; they can be simple or rather complex. How you use them depends greatly on what the program is trying to achieve; they could be the number of lives left in a game or just displaying a countdown.

# ## TRUE CONDITIONS

Keeping conditions simple to begin with makes learning to program a more enjoyable experience. Let’s start then by checking if something is TRUE, then doing something else if it isn’t.

**STEP 1** Let’s create a new Python program that will ask the user to input a word, then check it to see if it’s a four-letter word or not. Start with File > New File, and begin with the input variable:

```
~~~python
word=input("Please enter a four-letter word: ")
~~~
```

![](bbox=[0.06, 0.476, 0.47, 0.588])

**STEP 2** Now we can create a new variable, then use the len function and pass the word variable through it to get the total number of letters the user has entered:

```
~~~python
word=input("Please enter a four-letter word: ")
word_length=len(word)
~~~
```

![](bbox=[0.06, 0.724, 0.47, 0.838])

**STEP 3** Now you can use an if statement to check if the word_length variable is equal to four and print a friendly confirmation if it applies to the rule:

```
~~~python
word=input("Please enter a four-letter word: ")
word_length=len(word)
if word_length == 4:
    print(word, "is a four-letter word. Well done.")
~~~
```

The double equal sign (==) means check if something is equal to something else.

![](bbox=[0.49, 0.556, 0.933, 0.588])

**STEP 4** The colon at the end of if tells Python that if this statement is true do everything after the colon that’s indented. Next, move the cursor back to the beginning of the Editor:

```
~~~python
word=input("Please enter a four-letter word: ")
word_length=len(word)
if word_length == 4:
    print(word, "is a four-letter word. Well done.")
else:
    print(word, "is not a four-letter word.")
~~~
```

![](bbox=[0.49, 0.792, 0.933, 0.955])