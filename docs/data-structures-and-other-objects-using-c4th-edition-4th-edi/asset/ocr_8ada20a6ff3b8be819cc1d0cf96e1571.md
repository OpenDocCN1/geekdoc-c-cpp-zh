# PROGRAMMING EXAMPLE: Animal Guessing

Now we'll write a small program that uses the binary tree toolkit. The program is a simple guessing game: You pretend that you are an animal, and the program asks questions to try to guess what animal you are. If the program guesses correctly, another round of the game is started. And if the program can't figure out what you are, you provide some more knowledge to the program so that the next time the game is played, the program is a bit smarter.

As an example, suppose you are pretending to be a raccoon. The program might start by asking "Are you a mammal?" and you answer, "Yes." Next, the program wants to know "Are you bigger than a cat?" and again you answer, "Yes." Finally, the program guesses: "Are you a kangaroo?" and with a smug smile you reply, "No, don't be ridiculous."

an animal
guessing
program that
gets smarter and
smarter

At this point, the program says, "I give up. What are you?" You explain that you are a raccoon. You then provide the program with a question that the program can use in the future to distinguish a kangaroo from a raccoon—perhaps "Are you a marsupial?"—and you tell the program that the answer to this question is "yes" for a kangaroo but "no" for a raccoon. The next time that you are a raccoon, the program will have enough information to guess correctly. A sample dialogue with the program is given in Figure 10.7.

# FIGURE 10.7 Part of a Sample Dialogue with the Animal Guessing Program

```
A Sample Dialogue
Are you a mammal? Please answer [Yes or No]
Yes
Are you bigger than a cat? Please answer [Yes or No]
Yes
My guess is Kangaroo. Am I right? [Yes or No]
No
I give up. What are you?
Raccoon
Please type a yes/no question that will distinguish a Raccoon from a Kangaroo.
Your question:
Are you a marsupial?
As a Raccoon, Are you a marsupial? Please answer [Yes or No]
No
Shall we play again? [Yes or No]
No
Thank you for teaching me a thing or two.
```