
## CONTROL COMPONENTS

The beauty of the WPF template model is that you can make a control look almost any way you want it to, but all the functionality remains intact. If you were using most other UI platforms, you'd have to rebuild the control from scratch in order to do what we've been doing with a few lines of XAML. But the key word here is "almost". You might want your sliders to look like gauges (which would be cool, by the way), but there still has to be some way for the user to change the value. A TextBox isn't going to be too useful without some place to enter the text. A ComboBox...well, you get the idea.

ProgressBar has to have something to indicate progress and a track-y thing to indicate the 100%.

![](img/1dcd2af4ae4fa0eb5cf4ed5437ff121a_787_0.png)

![](img/1dcd2af4ae4fa0eb5cf4ed5437ff121a_787_1.png)

Slider has to have a button-y thing that can be moved, and a track-y thing that it can move along.

![](img/1dcd2af4ae4fa0eb5cf4ed5437ff121a_787_2.png)

ComboBox has to have someplace to display the selected content, someplace to display the list, and a button-y thing to control whether the list is displayed.

## CONTROL CONTRACTS

In earlier versions of the .NET Framework, the parts of a control that were required for it to function were implemented by setting the names of elements in the template to magic names that could be referenced by the functional code. It worked, but it was (to put it politely) painful. Just trying to figure out what controls need what parts and what those parts should be called could take the research skills of a PhD in Library Science. .NET 4.0 has made everybody's life easier by formalizing the ad hoc naming convention in a CONTROL CONTRACT that defines everything the template should include in order to function properly.

The control contract is defined using attributes. (We haven't worked with attributes since we looked at them back in Chapter 5, so you'll be forgiven for forgetting that they're a way of adding metadata to a code component.) Required control components, called PARTS, are implemented using the TemplatePartAttribute that has two required parameters: Name and Type. The value of the Name property is the x:Name you must use in your control template, and the value of Type is the type of control it needs to be. (These are usually defined at a pretty high level.)

![](img/1dcd2af4ae4fa0eb5cf4ed5437ff121a_788_0.png)

To make it even better, the contracts are actually documented in MSDN (Search for “Styles and Templates”, with the quotation marks.) It should lead you to the Control Styles & Templates section of the Library.

![](img/1dcd2af4ae4fa0eb5cf4ed5437ff121a_789_0.png)

But because the good people at MSDN have been known to move things around (usually the day after I find them), if all else fails, the control template attributes are included in the Class Library definition of the control.

![](img/1dcd2af4ae4fa0eb5cf4ed5437ff121a_789_1.png)

![](img/1dcd2af4ae4fa0eb5cf4ed5437ff121a_789_2.png)

## PUT ON YOUR THINKING HAT

Using either of these techniques, find out what the parts of a ProgressBar control are, and then write a snippet of XAML that defines the default visual tree of the control (Don’t worry about the VisualStateManager stuff. We’ll talk about that in the next section.)

For the sake of the exercise, assume that all the parts are implemented as instances of the Border class and contained in a Grid. You don’t need to make this too complicated; just figure out what parts need to be there and how they need to be named.

![](img/1dcd2af4ae4fa0eb5cf4ed5437ff121a_790_0.png)

## HOW'D YOU DO?

Here's my version.

```xml
<ControlTemplate TargetType="ProgressBar">
<Grid>
<Border x:Name="PART_Track" />
<Border x:Name="PART_Indicator" />
<Border x:Name="PART_GlowRect" />
</Grid>
</ControlTemplate>
```

![](img/1dcd2af4ae4fa0eb5cf4ed5437ff121a_790_1.png)

## MAKE A NOTE

I've been referring to the parts that are specified in the control template as “required components”, but in fact they aren’t all necessarily required. The ProgressBar is a good example. The PART_GlowRect is purely decorative, and if you leave it out, the control will still work just fine. Even parts that are functional can sometimes be left out. A scrollbar, for example, doesn’t need those little arrows that move the thumb by a small increment. The WPF controls are very smart about just ignoring parts that aren’t included in the template.

![](img/1dcd2af4ae4fa0eb5cf4ed5437ff121a_790_2.png)

## TAKE A BREAK

Lots of WPF elements include templates. The control template we’ve explored in this section is one of the most common, and we’ll look at data templates in the next chapter. But all of the templates work essentially the same way, so don’t panic if you run across one you haven’t seen before.

Now why don’t you take a break before you complete the Review and move on to the final section of this chapter: the VisualStateManager that takes the place of triggers in the control contract.

- What kind of Presenter do you use to display the Content property of a control?
- How would you declare an ellipse with a dashed outline?
- Control templates are typically placed in one of two places. What are those places and when would you use each?
- What's the difference between a Decorator and an Adorner?
- Why is it customary to put a Grid with one row and one column inside a Border?
- What element do you use to make a control template reflect the public properties of an element?
- What happens if you don't include one of the parts specified by a control's contract?

## VISUAL STATES

In the last chapter we used property and event triggers to define the visual behavior of a control. Inside a control template (and unfortunately only inside a control template) you have another, more powerful option: the VisualStateManager. Like control parts, the visual states that are supported by a control are defined by its control contract, using the TemplateVisualState attribute, which defines both the state and the state group:

```
[TemplateVisualState(Name="Normal", StateGroup="CommonStates")]
```

![](img/1dcd2af4ae4fa0eb5cf4ed5437ff121a_792_0.png)

- The visual states within a VisualStateGroup are mutually exclusive.
- At any given time, an element will be in one state from each VisualStateGroup.
- A VisualState element contains a Storyboard.
- The Storyboard contained in a VisualTransition will be activated when the element changes states.
- An element can contain any number of visual state groups, and each group can contain any number of visual states.

![](img/1dcd2af4ae4fa0eb5cf4ed5437ff121a_793_0.png)

## PUT ON YOUR THINKING HAT

The Button element has three state groups and a total of nine visual states, as shown below. Write a skeleton of a control template that defines each state. (You know how to do that, right?) Don't worry about the Storyboard right now.

| Visual State Group | Visual State |
|---|---|
| CommonStates | Normal |
| CommonStates | MouseOver |
| CommonStates | Pressed |
| CommonStates | Disabled |
| FocusStates | Focused |
| FocusStates | Unfocused |
| ValidationStates | Valid |
| ValidationStates | InvalidFocused |
| ValidationStates | InvalidUnfocused |

![](img/1dcd2af4ae4fa0eb5cf4ed5437ff121a_793_1.png)

## MAKE A NOTE

You can still use triggers inside a control template, and a lot of the samples you'll find on the Internet use this older technique. But when you're customizing controls that define visual states, you really should use the VisualStateManager instead because the controls are built to integrate with it, and you're likely to have more flexibility than you would with a pure trigger solution. Of course, you can always use both, if you want to respond to an event or property change that isn't covered by the states defined by the control.

![](img/1dcd2af4ae4fa0eb5cf4ed5437ff121a_794_0.png)

## HOW'D YOU DO?

Did you figure out that you specify the group and state names using the x:Name markup extension, or did you have to peek?

```xml
<ControlTemplate TargetType="Button">
... Visual Tree ...
<VisualStateManager.VisualStateGroups>
<VisualStateGroup x:Name="CommonStates">
<VisualState x:Name="Normal" />
<VisualState x:Name="MouseOver" />
<VisualState x:Name="Pressed" />
<VisualState x:Name="Disabled" />
</VisualStateGroup>
<VisualStateGroup x:Name="FocusStates">
<VisualState x:Name="Focused" />
<VisualState x:Name="Unfocused" />
</VisualStateGroup>
<VisualStateGroup x:Name="ValidationStates">
<VisualState x:Name="Valid" />
<VisualState x:Name="InvalidUnfocused" />
<VisualState x:Name="InvalidFocused" />
</VisualStateGroup>
</VisualStateManager.VisualStateGroups>
</ControlTemplate>
```

The VisualStateGroups collection isn't exposed directly; it's an attached property.

Each group and each state is identified by name.

![](img/1dcd2af4ae4fa0eb5cf4ed5437ff121a_794_1.png)

## MAKE A NOTE

Unlike the parts defined in the control template, the visual states supported by a control are only documented in the “Control Styles and Templates” section of MSDN, not in the class library. At least, that’s the case as I write this. It may be different tomorrow.
