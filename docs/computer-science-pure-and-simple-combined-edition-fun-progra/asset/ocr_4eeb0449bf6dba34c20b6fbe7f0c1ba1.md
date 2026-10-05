talkto "text1"

```
cleartext
talko "text2"
cleartext
talko "text3"
cleartext
end
```

to Start
Main
end

# #30 HANGMAN IV

```
to Main
local [counter letter1 letter2 letter3]
talko [t1 t2 t3 t4 t5 t6]
ht
reset
make "counter 0"
forever
question [Please give me a letter]
if (answer = "d")
talko "text1" print answer make "letter1" answer
if (answer = "o")
talko "text2" print answer make "letter2" answer
if (answer = "g")
talko "text3" print answer make "letter3" answer
show:
if not (or answer = "a")
[make sum "counter 1"]
if (counter = 1)
talko "t2 st stsh "nose"
if (counter = 2)
talko "t1 st stsh "head"
if (counter = 3)
talko "t3 st stsh "body"
if (counter = 4)
talko "t5 st stsh "arm2"
if (counter = 5)
talko "t4 st stsh "arm1"
if (counter = 6)
talko "t6 st stsh "legs"
if (counter = 6)
talko "you lose!" stop
[announce "You win!" stop]
if (answer = "d:letter2 = "o:letter3 = "g"
[announce "You win!" stop]
```

to Start
Main
end

```
to reset
talko "text1"
cleartext
talko "text2"
cleartext
talko "text3"
cleartext
end
```

EXERCISE 1: Change underlined lines.

```
to Main
local [counter letter1 letter2 letter3]
talko [t1 t2 t3 t4 t5 t6]
ht
reset
make "counter 0"
forever
question [Please give me a letter]
if (answer = "d")
talko "text1" print answer make "letter1" answer
if (answer = "o")
talko "text2" print answer make "letter2" answer
if (answer = "g")
talko "text3" print answer make "letter3" answer
show:
if not (or answer = "a")
[make sum "counter 1"]
if (counter = 1)
talko "t2 st stsh "nose"
if (counter = 2)
talko "t1 st stsh "head"
if (counter = 3)
talko "t3 st stsh "body"
if (counter = 4)
talko "t5 st stsh "arm2"
if (counter = 5)
talko "t4 st stsh "arm1"
if (counter = 6)
talko "t6 st stsh "legs"
if (counter = 6)
talko "you lose!" stop
[announce "You win!" stop]
if (answer = "d:letter2 = "o:letter3 = "g"
[announce "You win!" stop]
```

EXERCISE 2: Change this line near the end of Main, adding "win":

```
Add this procedure:
to win
talko [t1 t2 t3 t4 t5 t6]
ht
setsh [fire12]
repeat 30 [forward 0.01 wait 1]
end
```

# #31 CITY 1

```
to Main
talko "t1"
st
question [I will build you a house. Do you want big or small?]
else (answer = "big") [house 1]0.5]
wait 5
question [Do you want 1 or 2 windows?]
else (answer = 1) [window 1]window2
```

200