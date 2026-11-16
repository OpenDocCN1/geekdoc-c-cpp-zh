
## THE SOLUTION...

Compare the increasingly complex set of event handlers on the previous page to the same functionality implemented with WPF binding. All we have to do is specify the element and property we want, and WPF handles all the rest. I know which version I'd rather write.

This is our original version. We had to find change events we could use and track down some non-obvious bugs. And this is only three properties. What if you had twenty, or fifty? What about binding to a collection? It gets ugly fast.

```
private void Window_SizeChanged(object sender, SizeChangedEventArgs e)
{
    WidthLabel.Content = Box.ActualWidth.ToString();
    HeightLabel.Content = Box.ActualHeight.ToString();
}

private void Box_TextChanged(object sender, TextChangedEventArgs e)
{
    if (this.IsLoaded)
        TextLabel.Content = Box.Text;
}
```

Here's a version that uses WPF binding. All we need to do is add a markup extension to the XAML. (We could have done it in code instead, of course). That's all we ever have to do. In every situation. No hunting for an event we can hook on to, no tracking down weird and wonderful unrelated problems...

```
<TextBox x:Name="Box" .../>
<Label Content="{Binding ElementName=Box, Path=ActualWidth}" .../>
<Label Content="{Binding ElementName=Box, Path=ActualHeight}" .../>
<Label Content="{Binding ElementName=Box, Path=Text}" .../>
```

![](img/1dcd2af4ae4fa0eb5cf4ed5437ff121a_805_0.png)

## TASK LIST

We'll start this chapter by exploring the basics of WPF binding. You've already done some basic binding in other contexts, so this might seem like old news, but then we'll move on to some more interesting stuff, including how to convert and format the data, and how to bind to and navigate entire sets of data.

![](img/1dcd2af4ae4fa0eb5cf4ed5437ff121a_805_1.png)

## CREATING BINDINGS

Before we get into the complexities of WPF bindings, we need to get the basics down, so we'll start by looking at the basic objects involved and how to use them.

![](img/1dcd2af4ae4fa0eb5cf4ed5437ff121a_805_2.png)

## BINDING TO COLLECTIONS

Next we'll explore binding entire sets of data to items controls like the ListBox, ComboBox and TreeView. In order to use these controls effectively, you need to know how the data from the binding source is displayed, so we'll also examine data templates, which are just another form of the templates you learned how to build in the last chapter.

![](img/1dcd2af4ae4fa0eb5cf4ed5437ff121a_805_3.png)

## WORKING WITH COLLECTIONS

WPF provides some useful functions for working with collections of data. We'll start by exploring the Master-detail pattern that lets you display the details about an item selected in an items control, and then explore a few other useful tools in the binding toolbox, including how to filter, sort and group a set of data, and how to convert a value into a form that's more useful to you.

## CREATING BINDINGS

You've already written one kind of binding expression when you used the TemplateBinding element in a control template, but the general binding syntax is a little different, so let's start with a simple little example. (We'll be expanding it as we go along.)

This is a ListBox we'll be binding later in the chapter.

The elements in this column... ...are given the names in this column.

![](img/1dcd2af4ae4fa0eb5cf4ed5437ff121a_806_0.png)

We'll use the TextBox as the source for the label.

We'll be binding these labels as we go along.

```
{Binding ElementName="<name>", Path="<property>"}
```

## PUT ON YOUR THINKING HAT

Ready to get started? Here's a class diagram of the Binding object. Using it and the example from a couple of pages ago, can you do the following?

![](img/1dcd2af4ae4fa0eb5cf4ed5437ff121a_807_0.png)

- 1. Create a new project and build the basic form. Mine uses a Grid as the root element, with three columns and five rows, but you don't need to organize it that way if you have a better idea. Make sure you give the TextBox and the labels in the last column the names specified in the second column.
- 2. Set the binding for the Label1 named TextLabel1 so that it displays the contents of the TextBox.
- 3. Set the binding for the Label1 named FontLabel1 so that it displays the FontStyle of TextLabel1.
- Leave the GridLabel1 and Button for the time being; we'll fix them up later.
- 4. Run the application. When is the first TextBox updated? What property of the Binding object do you think you need to set to change this behavior?

## HOW'D YOU DO?

It's only fair to tell you that WPF binding can get pretty complicated, but most of the time, it's just this easy.

I've left out the XAML that just formats the Window so we can concentrate on the Binding elements.

```
<Window ... >
<Grid ... >
<Grid.ColumnDefinitions ... />
<Grid.RowDefinitions ... />
<ListBox ... />
<Label ...TextSource:...</Label>
<Label ...TextLabel...</Label>
<Label ...FontLabel...</Label>
<Label ...GridLabel...</Label>
<TextBox x:Name="TextSource" ...>Sample Text</TextBox>
<Label x:Name="TextLabel" Content="{Binding ElementName=TextSource, Path=Text}" />
<Label x:Name="FontLabel" Content="{Binding ElementName=TextLabel, Path=FontStyle}" />
<Label x:Name="GridLabel" ...>...bound value...</Label>
<Button x:Name="UpdateButton" ...>Update Now</Button>
</Grid>
</Window>
```

There are other options, and we'll look at a couple in a few pages, but the easiest way to bind to an element is by name.

Here are the lines that perform the binding. You had an example of the first one. Did you work out the second one?

## TAKE A BREAK

Bindings are a little complex, so why don't you take a break before we move on?

## BINDING MODES

In the exercise, I asked you to think about what property you might use to control when a binding target is updated. The answer is the UpdateSourceTrigger, which takes a member of the UpdateSourceTrigger enumeration. UpdateSourceTrigger is one of two properties that control how the Binding behaves. The other is the BindingMode, which determines how the source and target interact. We'll start by exploring the second property: BindingMode.

The BindingMode property controls the effect that the target and source have on one another.

You'll use TwoWay binding most of the time. It tells the Binding object to update both objects when either one changes.

OneWay binding means that the target has no effect on the source.

OneTime binding is more efficient when neither the source nor target changes. It sets the initial value, and then ignores any other changes.

![](img/1dcd2af4ae4fa0eb5cf4ed5437ff121a_809_0.png)

OneWayToSource doesn't make sense in many circumstances, but it can be used to trick WPF into performing a one-way binding to a non-dependency property by swapping the target and source. The technique is, at best, a kludge, but sometimes you have no choice.

![](img/1dcd2af4ae4fa0eb5cf4ed5437ff121a_809_1.png)

## UPDATE TRIGGERS

The other property that controls how the Binding behaves is the UpdateSourceTrigger that does exactly what the name implies: It defines when an update of the source is triggered. Don't confuse the UpdateSourceTrigger with style or event triggers. Like static properties and static resources, the terms mean different things.

UpdateSourceTrigger only applies when the source is actually being updated, which means the Mode must be TwoWay or OneWayToSource.

![](img/1dcd2af4ae4fa0eb5cf4ed5437ff121a_810_0.png)

When the UpdateSourceTrigger is set to Explicit, you have to call UpdateSource() on the BindingExpression. (Remember that WPF creates a BindingExpression whenever you link a Binding object to a property on the binding source. This allows you to re-use a Binding object for multiple source properties.)

The GetBindingExpression() method returns an instance of the BindingExpression for you to work with in code.

```
BindingExpression be = TextLabel1.GetBindingExpression(Label.ContentProperty);
be.UpdateSource();
```

Once you have a reference to the BindingExpression, the UpdateSource() method tells the Binding to perform the deferred update.

![](img/1dcd2af4ae4fa0eb5cf4ed5437ff121a_810_1.png)
