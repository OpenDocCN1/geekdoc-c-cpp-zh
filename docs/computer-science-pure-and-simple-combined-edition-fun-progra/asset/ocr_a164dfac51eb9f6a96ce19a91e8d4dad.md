# #13 Cool Animation

Load in your work
From the File menu, open your previous project named jump, the one with the running dog and the jump button. Then from the File menu select "Save Project As" and save your project as jump2.
In the Procedures Page, your program should look like this:

```
to Main
cc eg pu
talkto "t1"
setsh [dog1 dog2]
seth 270
repeat 200
  [Walk 10 10]
end

to doJump :height
local "originalY"
make "originalY" ycor
sety sum ycor :height
wait 1
sety :originalY
end

to jump
doJump 30
end

to Start
Main
end

to walk :stepsize :qsteps
repeat :qsteps
  [forward :stepsize]
  wait 1
end
```