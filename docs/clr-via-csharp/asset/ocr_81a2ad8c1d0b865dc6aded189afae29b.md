The reason, of course, is that someone can call the first method passing in an array object, a **List<T>** object, a **String** object, and so on—any object whose type implements **IEnumerable<T>**. The second method allows only **List<T>** objects to be passed in; it will not accept an array or a **String** object. Obviously, the first method is better because it is much more flexible and can be used in a much wider range of scenarios.

Naturally, if you are writing a method that requires a list (not just any enumerable object), then you should declare the parameter type as an **IList<T>**. You should still avoid declaring the parameter type as **List<T>**. Using **IList<T>** allows the caller to pass arrays and any other objects whose type implements **IList<T>**.

Note that my examples talked about collections, which are designed using an interface architecture. If we were talking about classes designed using a base class architecture, the concept still applies. So, for example, if I were implementing a method that processed bytes from a stream, we'd have this:

```
```csharp
// Desired: This method uses a weak parameter type
public void ProcessBytes(Stream someStream) { ... }

// Undesired: This method uses a strong parameter type
public void ProcessBytes(FileStream fileStream) { ... }
```
```

The first method can process bytes from any kind of stream: a **FileStream**, a **NetworkStream**, a **MemoryStream**, and so on. The second method can operate only on a **FileStream**, making it far more limited.

On the flip side, it is usually best to declare a method's return type by using the strongest type possible (trying not to commit yourself to a specific type). For example, it is better to declare a method that returns a **FileStream** object as opposed to returning a **Stream** object:

```
```csharp
// Desired: This method uses a strong return type
public FileStream OpenFile() { ... }

// Undesired: This method uses a weak return type
public Stream OpenFile() { ... }
```
```

Here, the first method is preferred because it allows the method's caller the option of treating the returned object as either a **FileStream** object or as a **Stream** object. Meanwhile, the second method requires that the caller treat the returned object as a **Stream** object. Basically, it is best to let the caller have as much flexibility as possible when calling a method, allowing the method to be used in the widest range of scenarios.

Sometimes you want to retain the ability to change the internal implementation of a method without affecting the callers. In the example just shown, the **OpenFile** method is unlikely to ever change its internal implementation to return anything other than a **FileStream** object (or an object whose type is derived from **FileStream**). However, if you have a method that returns a **List<String>** object, you might very well want to change the internal implementation of this method in the future so that it would instead return a **String[]**. In the cases