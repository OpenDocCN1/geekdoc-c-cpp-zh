to create several.

We need a list because we want to create five variables. Let's try this at the top of the madlibstest
procedure:

```
local [noun1 noun2 noun3 noun4 adj1 adv1]
```

In fact, it is standard procedure in programming to create your variables at the top of the procedure,
and then the rest of the coding. So let's plan to do that.

We need one more procedure that allows us to talk to the user. Let's try announce. The Help menu
tells us this:

```
announce
announce word-or-list
```

Displays the message in an alert box. Clicking OK closes the box. See question and answer.
So the input for announce can be a list of words in brackets. Let's test this in the Command Center:
announce [Here is your madlib.]

Does it work? Let's add these ideas to our madlibstest. We can use these new tools: question,
print, sentence, local using a list of variables, and announce.

```
To madlibstest
local [noun1 noun2 verb3 adj4 noun5]
question [Please type in an animal name.]
make "noun1 answer
announce [Here is your madlib.]
print (sentence [One the day]: :noun1 [took a walk in the rain].
end
```

# Planning

The next thing you need to do for our madlibs procedure is to write a simple story on a piece of
or in a word processor. Underline five words that you will be erasing, but don't choose verbs
(action words). Verbs are too hard to get when asking input from the user. Separately, write
down for each word. (Remember, the question needs to ask the user for a word of the
type, not exactly the same word, or the madlib won't end up being funny.) Keep the questions
er. Next to each question, write down a good variable name for that underlined word, for
example, noun1, noun2, noun3, adj1, adv1, and so on.

# Pseudocode

Pseudocode is just like program code except that it is written in English. It helps us make a quick
and easy plan without worrying yet about getting details exactly right.