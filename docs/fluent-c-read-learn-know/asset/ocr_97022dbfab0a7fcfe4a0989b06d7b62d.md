# COMBINING TRIGGERS & STYLES

Did you work out the rule that applies to both triggers and styles? Triggers beat Styles, and whenever there are two or more of either of them, the last one declared wins.

# AND THE WINNER IS...

Trigger 2. Even though Style B takes precedence over Style A because it is declared after it, Triggers take precedence over Styles, so the last applicable Trigger is applied.

| Style A |
| Trigger 1 |
| Trigger 2 |
| Style B |

Now, the examples we played with on the last page were a little silly. You wouldn’t define triggers for properties that aren’t mutually exclusive, or two implicit templates for the same element in a single file. If you did, it would be fairly easy to track down the problem. But this kind of thing can easily happen when you’re working with multiple ResourceDictionaries.

What’s a poor programmer to do? WPF is doing exactly what you told it to do (you just didn’t tell it what you thought you did), so sloppy debugging isn’t going to help you, but here are some tips:

# BE AWARE OF THE PROBLEM

Just knowing how this kind of thing happens can help a lot.

# MAKE IMPLICIT STYLES GENERIC

Your life will be easier if your implicit styles only set properties that really are valid for every instance of the element. I know the syntax for referencing a style is a bit ugly, and so it’s tempting to choose the “most used” style as the default, but that will cause problems in the long run. (Yes, you’re listening to the voice of experience.)

# ORGANIZE STYLES FROM MOST-GENERIC TO MOST-SPECIFIC

Try to organize styles from most-generic (basic color and font resources, for example) to most specific (styles that only apply in a few cases), and when you’re adding them to a merged dictionary, make sure you add them in that order. It’s not a perfect solution, but it will help prevent styles from stepping on one another.

![](bbox=[0.5, 0.73, 0.91, 0.92])