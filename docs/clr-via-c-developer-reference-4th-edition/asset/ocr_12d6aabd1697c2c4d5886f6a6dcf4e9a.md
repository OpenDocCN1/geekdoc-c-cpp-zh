Here, the first method preferred because it allows the method's caller the option of treating the returned object as either a FileStream object or as a Stream object. Meanwhile, the second method requires the caller treat the returned object as a Stream object. Basically, it is best to let the caller have as much flexibility as possible when calling a method, allowing the method to be used in the widest range of scenarios.

In this example you retain the ability to change the internal implementation of a method without affecting the callers. In the example just shown, the OpenFile method is unlikely to ever change its internal implementation to return anything other than a FileStream object (or an object whose type is derived from FileStream). However, if you have a method that returns a List<String>-object, you might very well change the internal implementation of the method in the future so that it would instead return a String[]. In the cases in which you leave yourself flexibility to change what your method returns, choose a weaker return type. This is an example:

+   - Flexible: This method uses a weaker return type
public IList<String> GetStringCollection() { }

+   - Inflexible: This method uses a stronger return type
public List<String> GetStringCollection() { }

In example, even though the GetStringCollection method uses a List<String> object internally and returns it, it is better to prototype the method as returning an IList<String> instead. In the future, the GetStringCollection method could change its internal content to use String[], and callers of the method won't be required to change any of their source code. In fact, they won't have to reconcile their code. Notice in this example that I'm using the strongest of the weakest types of code. For instance, I'm not using IEnumerable<String> or ICollection<String>.

# Const-ness

In some languages, as unmanaged C++, it is possible to declare methods or parameters as const that forbids the code in an instance method from changing any of the object's fields or prevents the code from modifying any of the objects passed into the method. The CLR does not provide for this feature, no language (including C#) can offer this feature.

First, you should note that in unmanaged C++, marking an instance method or parameter as const ensures that the programmer could write normal code that would modify the object or parameter. Inside the method, it was always possible to write code that could mutate the object/parameter by casting away the const address of the object/argument and then writing to the address. In a sense, unmanaged C++ lied to programmers, making them believe that their constant objects/arguments couldn't be written to even though they could.