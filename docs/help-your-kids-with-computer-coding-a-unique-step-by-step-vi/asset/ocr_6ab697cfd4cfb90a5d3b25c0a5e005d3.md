# Hide and seek

Welcome to the special effects studio! Using the purple
“Looks” blocks, find out how to make sprites vanish and
reappear, grow and shrink, and fade in out.

# Hiding sprites

To make a sprite disappear, use the "hide" block.
Theprite is still on the stage, and it can still move around,
but it can't be seen unless the "show" block is used to
make it visible again.

> SEE ALSO
- 38–39 Making things move
- 70–71 Sending messages

Use the "hide" block
to make sprites
disappear in games

+   - Hide and show
To make a sprite vanish, use the "hide"
block. When you're ready for it to be
seen again, use the "show" block.
These blocks are found in the "Looks"
section of the blocks palette.

![](bbox=[0.353, 0.287, 0.893, 0.53])

+   - Disappearing cat
Try this script using the cat sprite.
disappears and reappears but it keeps
moving, even when you can't see it.

> EXPERT TIPS
Showing sprites

Select a sprite in the sprite list.
Click the "i"button on it to open
the information panel. You can
also use the "show"tick box
to show or hide a sprite.

```
when clicked
forever
wait 1 secs
hide
turn 90 degrees
move 100 steps
wait 1 secs
show
```

This block hides
t cat
This block rotates
t cat clockwise
The cat still moves
even when hidden
This block shows
t cat again

```
Sprite1
x: 84 y: -69
rotation style: []
can drag in player: []
show: []
```

![](bbox=[0.626, 0.903, 0.933, 0.95])

Show a
hidden sprite