# MORE CLASSES

Did you notice something odd about the DependencyObject and PropertyMetadata classes? They descend directly from Object, not one of the WPF classes like FrameworkElement. I think of them as sitting outside the system in order to manipulate it. (I'm sure the architects of WPF would have a more elegant description.)

But the WPF classes you create will descend, more or less directly, from FrameworkElement, and one of the ancestors of FrameworkElement, the DependencyObject, provides some important functions for creating and working with dependency properties. In fact, DependencyObject, which as you can see sits quite high in the WPF class hierarchy, specifically encapsulates the functionality of objects that participate in the dependency property system.

A DependencyObjectType links a specific CLR type to the dependency property system. It's really just glue that you don't need to worry about.

ClearValue() clears any local values that have been explicitly set, but not values applied further up the calculation chain.

![](bbox=[0.45, 0.36, 0.8, 0.6])

You'll only have to call CoerceValue() explicitly in very rare situations.

Don't try to use OnPropertyChanged to respond to a property change event. Instead, use the PropertyChangedCallback.

SetValue() and GetValue() are used inside the CLR property definition to make sure the backing property stays synchronized with the dependency property system.

InvalidateProperty() forces the value of the property to be recalculated.