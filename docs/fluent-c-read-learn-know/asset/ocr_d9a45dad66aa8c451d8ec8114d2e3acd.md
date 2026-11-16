# CONTROL TEMPLATES

Now that we've seen some of the most common elements you'll use to define the visual tree of your control, let's look at the syntax for actually doing so using a control template.

Control templates can be defined as a resource or (more commonly) as part of a style. The syntax probably won't come as a great surprise to you.

You can define the control template of an individual element:

```
<Button>
<Button.Template>
<ControlTemplate TargetType="Button">
<ControlTemplate.Triggers>
... property and event triggers ...
</ControlTemplate.Triggers>
... Visual Tree ...
<VisualStateManager.VisualStateGroups>
... Visual States & Transitions ....
</VisualStateManager.VisualStateGroup>
</ControlTemplate>
</Button.Template>
</Button>
```

Like a content control, a control template must have a single child element, which can in turn contain other elements.

You must specify the target type, even within an element definition.

Templates have a Triggers collection, just like a Style.

We'll talk about the VisualStateManager later in this chapter.

But it's usually done inside a style so it's available to multiple elements:

The control template is set inside a normal property setter.

```
<Style TargetType="Button">
...
<Setter Property="Template">
<Setter.Value>
<ControlTemplate TargetType="Button">
...
</ControlTemplate>
</Setter.Value>
</Setter>
</Style>
```

You always need to specify the TargetType.