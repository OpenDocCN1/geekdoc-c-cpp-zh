# # Appendix II

# # Part 1 Answers

Note: Many answers are contained in the text. This key contains those that are not in the text.

becomes

to square

# #2 answers

```
To square
;draws a square of 50 units
pd
repeat 4 [forward 50 right 90 wait 1]
end
```

```
;draws a square of 50 units
pd
repeat 4 [forward 50 right 90 wait 1]
end
```

Drawing a starburst

to starburst

```
repeat 360 [right 1 forward 50 back 50]
end
```

# #4 answers

Drawing a triangle

to triangle

```
to Main
ce
pu
talkto "ti"
works with turtle named tl
seth [dog1 dog2] or [doggy dog2]
set -90
repeat 20 [fd 2 wait 2]
end
```

```
;draws a triangle of 3 sides of 50
pd
repeat 3 [forward 50 right 120 wait 1]
end
climb.to.roof
;takes turtle position to draw roof
pd
set 0
forward 50
right 30
pd
end
```

```
to square
;draws a square of 50 units
pd
repeat 4 [forward 50 right 90 wait 1]
end
```

```
to Main
;draws a simple house
eeg
pd
square
climb.to.roof
triangle
end
```

```
to Start
Main
end
```

```
to square
:draws a square of 50 units
pd
forward 50 right 90 wait 1
forward 50 right 90 wait 1
forward 50 right 90 wait 1
forward 50 right 90 wait 1
end
```

# #5 answers

# #6 answers (procedures in alphabetical order)

```
to Main
;draws a house
eeg
pd
square
```