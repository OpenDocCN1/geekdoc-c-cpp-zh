# EXERCISE 2, ONE QUESTION GUESSING GAME:

to Main
oneq
end

to intro
question [What's your name?]; makes a dialogue box
announcement [I like your name.] : dialogue box without space
question [Would you like to play One Question? Y or N]
else (answer = 'y') [oneq] [announcement [Bye!]]
end

to oneq
local "quiznumber"
make "quiznumber 4"
question (Guess :quiznumber between 0 and 10.)
if (answer > :quiznumber) [announcement [Too big!]]
if (answer < :quiznumber) [announcement [Too small!]]
if (answer = :quiznumber) [announcement [You got it!]]
print (sentence [The number was]: :quiznumber)
end

to Start
Main
end

if (answer > :quiznumber) [announcement [Too big!]]
if (answer < :quiznumber) [announcement [Too small!]]
if (answer = :quiznumber) [jig]
print (sentence [The number was]: :quiznumber)
end

to Start
Main
end

# #18 WANDERING TURTLE SOLUTIONS

to Main
repeat 60
[wander 5]
end

to :stepSize
turn right by a random amount which could be negative
right difference random 100 50
move forward by stepSize, twice
repeat 2 [for:stepSize wait 1]
end

to Start
Main
end

# #17 ANIMATION USING VARIABLES SOLUTIONS

EXERCISE 2, GUESSING GAME WITH JIG ADDED:

to Main
intro
end

to intro
question [What's your name?]; makes a dialogue box
announcement [I like your name.] : dialogue box without space
question [Would you like to play One Question? Y or N]
else (answer = 'Y') [announcement [Bye!]]
end

to jig
announcement [You got it!]
talkto "ti"
pd
repeat 30 [fd 2 wait 1 right 10 fd 4 wait 1 left 25]
end

to oneq
local "quiznumber"
make "quiznumber 4"
question (Guess a number between 0 and 10.)

to Main
setshh [horse1 horse2 horse3]
repeat 60 [wander 5]
end

to Start
Main
end

+   1. Adjust the stepSize. Change wander 5 to whatever.
2. Adjust the input to make smoother lines. How do you do that?
Change the input to random. How do you want to adjust the number subtracted from the random number? Make it half the input to random. For example, difference random 100 50 can become difference random 40 20
3. Make the turtle's shape change as it wanders around. Hint: use set in Main. See below.

to :stepSize
pd
turn right by a random amount which could be negative
right difference random 100 50
move forward by stepSize, twice
repeat 2 [for:stepSize wait 1]
end

193