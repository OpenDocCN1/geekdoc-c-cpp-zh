
## THE BASE VALUE

The first step a dependency property performs in calculating its final value is to determine its base value. Like a standard .NET property, the process starts with a default value, but a dependency property has a whole bunch more steps (most of which we won't talk about for a chapter or two. Sorry.)

![](img/1dcd2af4ae4fa0eb5cf4ed5437ff121a_605_0.png)

At the lowest level is the default value that's declared when the dependency property is created.

Values that are inherited from a parent, like the FontFamily that's set for the Window, take precedence over default values.

WPF THEMES are just like Windows themes—they are a collection of visual characteristics that are applied application-wide. We'll talk about them in Chapter 20.

A SETTER defines the value of a property as part of a style or template. We'll explore setters in Chapter 20.

A WPF STYLE defines the appearance of a particular type of control. We'll discuss styles in Chapter 20.

A TRIGGER changes the value of a property based on some condition, like displaying negative values in red. We'll explore triggers in Chapter 20.

A TEMPLATE defines how a control is composed. We'll discuss templates in Chapter 21.

When you set a property value explicitly it sets that LOCAL VALUE and trumps any other for the base value.

## AN EXAMPLE

This all seems really complicated, doesn't it? Relax. In practice, using dependency properties is pretty simple. Let's look at an example:

![](img/1dcd2af4ae4fa0eb5cf4ed5437ff121a_606_0.png)

Don't worry about how this Style is defined. We'll look at how styles work in Chapter 20.

- 1. Default Value: The default value of FontStretch is Normal.
- 2. Inherited Value: The Label inherits the value of Expanded from the Window that contains it.
- 3. Theme styles: This snippet doesn't have a theme so this step doesn't apply.
- 4. Theme Triggers: This snippet doesn't have a theme so this step doesn't apply.
- 5. Style setters: The style sets the FontStretch property to Condensed.
- 6. Template Triggers: This snippet doesn't have a template so this step doesn't apply.
- 7. Style Triggers: This style doesn't have a trigger so this step doesn't apply.
- 8. Local Value: This Label element sets the FontStretch to Medium.

And the final value of the Label.FontStretch property? It's Medium, the local value, which always trumps any other source.

## PUT ON YOUR THINKING HAT

Let's try a little dependency property experiment.

By default, when you create a new WPF window, the FontFamily attribute will be set to the default system font. That's Tahoma on XP, and Segoe UI (which, by the way, is pronounced "see-go") on Vista and Windows 7. The FontSize defaults to 9pt, and the Background to White.

These aren't bad choices. But they're not the only ones, and they may not be the most appropriate for your application. So, suppose you want your text to display in Times New Roman at 14 point in dark brown on a pale yellow background. Because dependency properties inherit their values, you should be able to set the font properties for the window, right? Here's a simple example:

```
<Window ...>
    FontFamily="Times New Roman" FontSize="14"
    Foreground="SaddleBrown" Background="Cornsilk" >
    <StackPanel>
        <Label>Hello, properties!</Label>
        <TextBlock>How are you doing today?</TextBlock>
    </StackPanel>
</Window>
```

Before you create the application, take a minute to think about what you expect to have happen:

What text and brush values do you think will be displayed in the Properties window for the Label and TextBlock controls? How do you expect them to display? Will they use the values set for the Window, or the default properties? Will both controls behave the same?

Okay, now create the Window and see what really happens.

## HOW'D YOU DO?

Okay, so dependency property value calculations don't always work the way we expect them to. Usually, but not always. So what happened and why?

Foreground, Background, FontFamily and FontSize are all dependency properties, but while the TextBlock inherits all the values from the Window, the Label only inherits the FontFamily and FontSize properties.

The reason for the inconsistent behavior is that all of the standard WPF controls have implicit default styles, and the default style for a Label sets the Foreground property. If you look back to the diagram of how values are calculated, you'll see that styles have a priority of 5 or 7, while inherited values only have a 2, so the style settings win.

Even once we've explored WPF styles in Chapter 20, you'll occasionally be surprised by this kind of thing. (And yes, once more, that's the voice of experience.) So what's a poor programmer to do? Take control. Either define your own control styles (probably the best solution in the long run) or set the value explicitly.

We'll look at WPF styles in detail in Chapter 20. Basically, they're just property settings that are grouped together and can be applied to more than one object.

![](img/1dcd2af4ae4fa0eb5cf4ed5437ff121a_608_1.png)

![](img/1dcd2af4ae4fa0eb5cf4ed5437ff121a_608_2.png)

## TAKE A BREAK

The final value of a dependency property can be determined by a lot of things, and as we've just seen, every once in a while that final value won't be what you were expecting. But these occasions really are pretty rare, and now that you've seen the pipeline, you know how to address them. So for now, why don't you take a break before completing the Review?

What does POCO stand for?

What does it mean to say that a dependency property “wraps” a POCO property?

What value always trumps the base value calculation?

What are the values of the FontFamily properties for the two labels in the following snippet?

```xml
<Window . .
   FontFamily="Times New Roman">
   <StackPanel>
   <Label Name="Label1">Hello</Label>
   <Label Name="Label2 FontFamily="Tahoma">World</Label>
   </StackPanel>
</Window>
```

## DEPENDENCY PROPERTY CLASSES

The keys to the WPF dependency property system are the DependencyProperty and PropertyMetadata classes that encapsulate all the functionality required to extend the behavior of a POCO property. Most of the members of these classes are self-explanatory. They’re all read-only values that are established when the dependency property is registered with the system by calling one of the Register...() methods. We’ll look at those at a minute, but first let’s look at the classes themselves.

UnsetValue and GlobalIndex are used internally by the dependency property system. You can safely ignore them.

This is the Type of the CLR property wrapped by the dependency property.

![](img/1dcd2af4ae4fa0eb5cf4ed5437ff121a_610_0.png)

This is the Type of the class that registered the dependency property.

A CALLBACK is a method that gets called whenever something occurs. If you specify values for these three properties, they’ll be called by the system whenever the value of the property is changed. We’ll talk about callbacks later in this chapter.

You can override the DefaultMetadata values using this method, but only in a static constructor for a class that inherits the property. (You’ll hardly ever do this.)

Most of these properties are used by panels to display their contents correctly. The exceptions are the binding properties, which we’ll discuss in Chapter 22, and the Inherits property, which determines whether the property can inherit values from its parent.

## MORE CLASSES

Did you notice something odd about the DependencyObject and PropertyMetadata classes? They descend directly from Object, not one of the WPF classes like FrameworkElement. I think of them as sitting outside the system in order to manipulate it. (I'm sure the architects of WPF would have a more elegant description.)

But the WPF classes you create will descend, more or less directly, from FrameworkElement, and one of the ancestors of FrameworkElement, the DependencyObject, provides some important functions for creating and working with dependency properties. In fact, DependencyObject, which as you can see sits quite high in the WPF class hierarchy, specifically encapsulates the functionality of objects that participate in the dependency property system.

A DependencyObjectType links a specific CLR type to the dependency property system. It's really just glue that you don't need to worry about.

ClearValue() clears any local values that have been explicitly set, but not values applied further up the calculation chain.

![](img/1dcd2af4ae4fa0eb5cf4ed5437ff121a_611_0.png)

You'll only have to call CoerceValue() explicitly in very rare situations.

Don't try to use OnPropertyChanged to respond to a property change event. Instead, use the PropertyChangedCallback.

SetValue() and GetValue() are used inside the CLR property definition to make sure the backing property stays synchronized with the dependency property system.

InvalidateProperty() forces the value of the property to be recalculated.
