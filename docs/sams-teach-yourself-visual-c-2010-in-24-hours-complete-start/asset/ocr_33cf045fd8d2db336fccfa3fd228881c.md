# ## Answers

+   1. Arrays are implicitly an instance of a System.Array object, so they are reference types, and the memory allocated to refer to the array itself is allocated on the managed heap. However, the elements of the array are allocated based on their own type.

+   2. The modifiers allowed for an indexer are new, virtual, sealed, override, abstract, and a valid combination of the four access modifiers.

+   3. List<T> is not designed to be easily extended because there are no virtual members that a derived class can override to modify behavior. Collection<T> does have virtual members that can be overridden, so Collection<T> is preferred when you need to customize behavior of the collection.

+   4. When the elements of a dictionary are enumerated, the dictionary returns a KeyValuePair<TKey, TValue> structure that represents a key and its associated value.

+   5. The Stack<T> class provides the Clear, Pop, and Push methods that remove all elements, remove the top element, or insert an element.

+   6. IDictionary<TKey, TValue> extends the ICollection<T> interface.

+   7. IComparer<T> defines a method to compare two objects, whereas IEqualityComparer<T> provides a way for you to provide your own definition of equality for type T.

+   8. Yes, collection initializers can be used with collections whose Add method takes more than one parameter.

# ## Exercises

+   1. Add a new public class named PhotoCollection that derives from ObservableCollection<IPhoto>. This class should have a string field named directory, a public constructor that accepts a string parameter and sets the field to the parameter value, and a public property named Path that gets or sets the value of the directory field.

+   2. Add a private PhotoCollection field named photos and a read-only property named Photos to the MainWindow class. In the constructor of the MainWindow class, add a statement that will assign a new PhotoCollection instance to the photos field.