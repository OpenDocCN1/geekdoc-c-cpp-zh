# INSTANTIATING A GENERIC

You know how to use standard parameters that allow you to specify a value at runtime, like as the String to be displayed in the MessageBox or the Int32 Capacity of a new ArrayList. Generics are also a kind of parameter, but instead of specifying a value, they specify a type.

The ArrayList contains instances of System.Object, and it always casts whatever you pass it to that type. We've seen that that's time-consuming and error-prone. (There's nothing to prevent you from adding objects of different types to the set, and that will come back to bite you.) List<T> is the generic equivalent of the ArrayList. It can do almost everything ArrayList can do, and some more besides, but because you specify the type at runtime, it doesn't have to cast everything to System.Object.

Notice the <T>. That's the syntax for a generic parameter. The angle brackets are required to specify a generic. The "T" is a convention. (It stands for "Type".) At runtime, you treat a generic parameter like any parameter—replace it with an appropriate value. The only difference is that "appropriate value" in this case means the name of a type:

![](bbox=[0.13, 0.44, 0.83, 0.7])