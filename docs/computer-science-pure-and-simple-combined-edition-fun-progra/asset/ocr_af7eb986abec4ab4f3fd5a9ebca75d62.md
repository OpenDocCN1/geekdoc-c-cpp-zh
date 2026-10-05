make "age 13
;put test sentence (shown below) here
end

To test each one, make sure you have a text box. Then type test in the Command Center to run the
test procedure. You don't have to keep typing test; just put the cursor right after the word and press
Enter. When it will run it. Here are your test sentences:

```
print (sentence "the :animal :ran")nprint (sentence [The very large]:animal [ran through the woods])
print [Hello there] [How are you?]
print sentence [Hello there] [How are you?]
print (sentence [Hello there] [How are you] [today?]
print (sentence [My age is | :age.years.])
```

For grins, change the animal and the age in the variables and run them again. You could make a
very large mouse run through the woods!

Now we know more on this subject, let's get interactive and collect those variable contents
from the user. In our madlistbest procedure on the Procedures Page, add these underlined lines:

+   To madlistbest
local "noun1"
question [Please type in an animal name.]
make "noun1" answer
show :noun1
print (sentence "hello :there :noun1")
print (sentence [What are we talking about?] :noun1)
end

Now go to the Command Center and type madlistbest. Press Enter.
What do you get? Do some more experimenting.
We're well on our way to making a madlib!

Now, if we want to create several variables at once? We'll need at least five variables. Let's
guss that local might be able to help us. Look up local under the Help index. It says this:

```
local
local word-or-list
```

We can use either a single word (with quote mark) or a list (with square brackets) as an input for
local. For instance, we can say:

```
local "fred
```

to create one variable, or

```
local [fred sam bob]
```