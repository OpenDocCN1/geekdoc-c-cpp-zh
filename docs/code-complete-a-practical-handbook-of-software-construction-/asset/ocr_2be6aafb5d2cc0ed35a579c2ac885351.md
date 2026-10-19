# Keep Variables “Live” for as Short a Time as Possible

A concept that’s related to variable span is variable “live time,” the total number of statements over which a variable is live. A variable’s life begins at the first statement in which it’s referenced; its life ends at the last statement in which it’s referenced.

Unlike span, live time isn’t affected by how many times the variable is used between the first and last times it’s referenced. If the variable is first referenced on line 1 and last referenced on line 25, it has a live time of 25 statements. If those are the only two lines in which it’s used, it has an average span of 23 statements. If the variable were used on every line from line 1 through line 25, it would have an average span of 0 statements, but it would still have a live time of 25 statements. Figure 10-1 illustrates both span and live time.

![](bbox=[0.2, 0.33, 0.8, 0.53])

![](bbox=[0.35, 0.55, 0.75, 0.75])

Figure 10-1 “Long live time” means that a variable is live over the course of many statements. “Short live time” means it’s live for only a few statements. “Span” refers to how close together the references to a variable are.

As with span, the goal with respect to live time is to keep the number low, to keep a variable live for as short a time as possible. And as with span, the basic advantage of maintaining a low number is that it reduces the window of vulnerability. You reduce