# to Main

talkto "t1
launch [repeat 2000 [forward 3 direct reach ||
when [touching] "t1 [t2] [win]
waituntil [colorder = 15]
announce [You lose!]
reset
end

to direct:key
if (ascii:key) = 28 [seth 270 0 fd 1]
if (ascii:key) = 29 [seth 90 0 fd 1]
if (ascii:key) = 30 [seth 0 0 fd 1]
if (ascii:key) = 31 [seth 180 0 fd 1]
if (ascii:key) = 37 [seth 270 0 fd 1]
if (ascii:key) = 39 [seth 90 0 fd 1]
if (ascii:key) = 40 [seth 180 0 fd 1]
if (key = "s") [stopall]
end

to go
to Main
announce [You win!]
talko "t1"
setsh cloud wait 2
setsh random 10 wait 10
end

to reset
talko "t1"
setpos [-319 -164]
end

+   4. Change win to this, adding underlined line:
to win
announce [You win!]
talko "t1"
setsh cloud wait 2
setsh random 10 wait 10
end

Change win to, adding underlined line:
to reset
talko "t1"
setpos [-319 -164]
seth 0
setsh 0
end

+   5. Add flow chart to describe what we have so far:

![](bbox=[0.535, 0.055, 0.865, 0.295])

# to Main

local "preference"
anounce "t1" If you go to the castle, you will be changed
into a man.
question [Would you like to be a prince or a princess? B for
boy or girl for the castle]
else (answer = "B") make "preference" [41]
talko "t1"
launch [repeat 2000 [forward 3 direct reach ||
when [touching] "t1 [t2] [win "preference]
waituntil [colorder = 15]
announce [You lose!]
end

> PRINCE PROJECT: Game asks the user whether the
user would be a prince or a princess, and the turtle turns into
boy or girl when it goes to the castle. If you have MicroWorlds EX,
 a boy shape into blank number 41, and a girl shape into
number 40. If you have MicroWorlds 2.0, use clear instead of
lightning!

to direct:key
if (ascii:key) = 28 [seth 270 0 fd 1]
if (ascii:key) = 29 [seth 90 0 fd 1]
if (ascii:key) = 30 [seth 0 0 fd 1]
if (ascii:key) = 31 [seth 180 0 fd 1]
if (ascii:key) = 37 [seth 270 0 fd 1]
if (ascii:key) = 39 [seth 90 0 fd 1]
if (ascii:key) = 38 [seth 0 0 fd 1]
if (ascii:key) = 40 [seth 180 0 fd 1]
if (key = "s") [stopall]
end