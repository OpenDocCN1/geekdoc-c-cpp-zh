```
to doJump :height
local "originalY"
make "originalY" ycor
set y sum ycor :height
wait 1
set y :originalY
end
```

Does it work? How do you change the height of the jump? Remember, you do it by changing the number used when calling doJump from Jump.

I like it! I like our new version of doJump, and it has fixed the "climbing up" problem. Time to tidy our program and save it. Here is my version:

```
to Main
cc cg pu
talkto "t1"
setsh [dog1 dog2]
set 270
repeat 200
[Walk 10 10]
end
```

```
to doJump :height
local "originalY"
make "originalY" ycor
set y sum ycor :height
wait 1
set y :originalY
end
```

```
to jump
doJump 40
end
```

```
to Start
Main
end
```

```
to walk :stepsize :steps
repeat :steps
[forward :stepsize
wait 1]
end
```