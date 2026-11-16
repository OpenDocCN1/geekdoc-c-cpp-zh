# VISUAL STATES

In the last chapter we used property and event triggers to define the visual behavior of a control. Inside a control template (and unfortunately only inside a control template) you have another, more powerful option: the VisualStateManager. Like control parts, the visual states that are supported by a control are defined by its control contract, using the TemplateVisualState attribute, which defines both the state and the state group:

```
[TemplateVisualState(Name="Normal", StateGroup="CommonStates")]
```

![](bbox=[0.27, 0.3, 0.71, 0.75])

The visual states within a VisualStateGroup are mutually exclusive.

At any given time, an element will be in one state from each VisualStateGroup.

A VisualState element contains a Storyboard.

The Storyboard contained in a VisualTransition will be activated when the element changes states.

An element can contain any number of visual state groups, and each group can contain any number of visual states.