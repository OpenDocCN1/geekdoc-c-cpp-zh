use the data-binding capabilities of WPF so that any time the photos. Path property changed the ImagesDirectory. Content property would automatically reflect that change.

This is accomplished easily by adding the following attribute to the XAML for the ImagesDirectory Label:

```
Content="{Binding Path=Path}"
```

This attribute tells the Label that the Content property is bound to some object that has a property named Path.

Next, you need to modify the set accessor of the Path property so that it provides a notification when its value changes. You can do this by adding the following line just after setting the directoryInfo field:

```
this.OnPropertyChanged (new PropertyChangedEventArgs ("Path"));
```

# Did you Know?

# The INotifyPropertyChanged Interface

Because the PhotoCollection class derives from ObservableCollection< T >, it already includes the necessary System. ComponentModel. INotifyPropertyChanged interface. This interface defines a single public event: the PropertyChanged event. You can use this interface in your own classes as well. Typically, you would implement the necessary event and an event handler similar to what is shown here:

```
protected virtual void OnPropertyChanged (PropertyChangedEventArgs e)  
{  
if (this.PropertyChanged != null)  
{
this.PropertyChanged (this, e);
}
}
```

Any property that should notify when its value has changed would call the OnPropertyChanged method.

If you look closely, you notice that the source object is not specified; but the source object is one of the four required components. In fact, without a binding source specified, the binding would actually do nothing.

How does this work? When the binding engine encounters a binding that has not specified a source, it looks upward through the hierarchy of visual elements looking for a DataContext. When it finds a DataContext, it uses that as the binding source.