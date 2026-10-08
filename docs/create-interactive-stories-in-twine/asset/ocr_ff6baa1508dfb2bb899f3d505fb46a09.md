# # Instructions

On the story map, click the test button. This will launch your game—but you'll also see a new section in the lower right corner:

| $fear | the number 0 |
| Turns: | 1 Abandoned Field | Debug View | 1 Variable |

The top part shows your variables. You should see the $fear variable you set on the left and the number value 0 on the right. If you do, you're in great shape!

In case you were wondering what the other elements were, I'll give you a quick rundown. Below the variables, you can track how many turns have passed. Each action a player takes—clicking and moving between passages—uses a turn. This debug view will show more information about the macros and backend in the passage. The variable button will toggle on and off displaying the variables.

Okay, now that we know our variable is working, let's use it! Close the testing tab and go back to the story map. Once you're there, edit the “Front of the House” passage.

If you remember, that was kind of a spooky place, and being there should definitely raise the fear level of the players. Now, we're going to use the set macro in this passage to add 1 fear whenever the players come here.

At the bottom of the passage, add the following:

```
(set: $fear to +1)
```

This macro says that it's going to add 1 to whatever the current value of $fear is. We set the $fear value to 0 in the “Variable” passage, the first time the players go here, their $fear value should go up to 1. If they left and came back, it would go up to 2.