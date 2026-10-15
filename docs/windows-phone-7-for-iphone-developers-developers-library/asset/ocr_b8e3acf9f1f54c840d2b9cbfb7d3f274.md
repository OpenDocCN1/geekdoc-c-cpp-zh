The key line here is the binding expression {Binding Main, Source={StaticResource Locator}}. This line is declaring that I want the data context of my entire view to be set to the Main property on the Locator object, which is a global resource. The MVVM Light project template put some code in our App.xaml file that declares an instance of the ViewModelLocator class as a global resource:

```
<Application.Resources>
    <vm:ViewModelLocator x:Key="Locator"
        d:IsDataSource="True" />
</Application.Resources>
```

Now that we have a view model locator, and our view’s data context has been set to an instance of a view model (remember, even though it’s an instance property it’s still pointing to a static singleton), we can bind some of our UI to the view model, as shown next:

```
<TextBlock x:Name="ApplicationTitle"
    Text="{Binding ApplicationTitle}"
    Style="{StaticResource PhoneTextNormalStyle}" />
<TextBlock x:Name="PageTitle"
    Text="{Binding PageName}"
    Margin="-3,-8,0,0"
    Style="{StaticResource PhoneTextTitle1Style}" />
```

The first phase of our adoption of MVVM is complete: the use of a view model. At this point a lot of developers and many architects sit back and think: Was this trip really necessary?

The answer is no. And yes. As I mentioned before, you can rig all this up spaghetti-style or you can do everything in code-behind. All we’ve done so far is provide a means for our application to make use of view models. So far you haven’t seen any of the real benefits because you’ve seen data binding before and it shouldn’t be that new to you. What comes next are the features of the MVVM Light toolkit and the benefits of MVVM adoption that could (and I’m not joking) change the way you write applications forever.

# Yes, But Will It Blend?

Developers familiar with building applications for the iPhone and iPad are intimately familiar with this problem: The design surface almost never reflects an accurate representation of the live, running application. It depends on the individual developer, but often the design surface experience of Interface Builder is so completely different from the runtime experience (especially when dealing with custom views with custom rendering) that developers simply skip IB entirely and do everything in code.

This is also true, to an extent, with Silverlight, WPF, and Windows Phone 7 applications. It is very easy to build an application that is so unfriendly to design tools that developers ignore the fact that design tools exist, and they do all their UI building the “notepad way”—by hand-entering XAML into Visual Studio.