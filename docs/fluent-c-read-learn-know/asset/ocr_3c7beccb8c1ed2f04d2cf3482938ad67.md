![](bbox=[0.11, 0.07, 0.23, 0.24])

# HOW'D YOU DO?

Here's my version.

```
```xml
<ControlTemplate TargetType="ProgressBar">
<Grid>
<Border x:Name="PART_Track" />
<Border x:Name="PART_Indicator" />
<Border x:Name="PART_GlowRect" />
</Grid>
</ControlTemplate>
```
```

![](bbox=[0.11, 0.42, 0.23, 0.59])

# MAKE A NOTE

I've been referring to the parts that are specified in the control template as “required components”, but in fact they aren’t all necessarily required. The ProgressBar is a good example. The PART_GlowRect is purely decorative, and if you leave it out, the control will still work just fine. Even parts that are functional can sometimes be left out. A scrollbar, for example, doesn’t need those little arrows that move the thumb by a small increment. The WPF controls are very smart about just ignoring parts that aren’t included in the template.

![](bbox=[0.11, 0.67, 0.23, 0.84])

# TAKE A BREAK

Lots of WPF elements include templates. The control template we’ve explored in this section is one of the most common, and we’ll look at data templates in the next chapter. But all of the templates work essentially the same way, so don’t panic if you run across one you haven’t seen before.

Now why don’t you take a break before you complete the Review and move on to the final section of this chapter: the VisualStateManager that takes the place of triggers in the control contract.