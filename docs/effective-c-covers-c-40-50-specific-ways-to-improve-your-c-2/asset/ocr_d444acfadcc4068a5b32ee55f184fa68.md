```
}
// TODO: free unmanaged resources here.

// Let the base class free its resources.
// Base class is responsible for calling
// GC.SuppressFinalize ( )
base.Dispose(isDisposing);

// Set derived class disposed flag:
disposed = true;
}
}
```

Notice that both the base class and the derived class contain a flag for the disposed state of the object. This is purely defensive. Duplicating the flag encapsulates any possible mistakes made while disposing of an object to only the one type, not all types that make up an object.

You need to write Dispose and finalize defensively. Disposing of objects can happen in any order. You will encounter cases in which one of the member objects in your type is already disposed of before your Dispose() method gets called. You should not view that as a problem because the Dispose() method can be called multiple times. If it's called on an object that has already been disposed of, it does nothing. Finalizers have similar rules. Any object that you reference is still in memory, so you don't need to check null references. However, any object that you reference might be disposed of. It might also have already been finalized.

You'll notice that neither MyResourceHog nor DerivedResourceHog contain a finalizer. The example code I wrote does not directly contain any unmanaged resources. Therefore, a finalizer is not needed. That means the example code never calls Dispose(false). That's the correct pattern. Unless your class directly contains unmanaged resources, you should not implement a finalizer. Only those classes that directly contain an unmanaged resource should implement the finalizer and add that overhead. Even if it's never called, the presence of a finalizer does introduce a rather large performance penalty for your types. Unless your type needs the finalizer, don't add it. However, you should still implement the pattern correctly so that if any derived classes do add unmanaged resources, they can add the finalizer, and implement Dispose(bool) in such a way that unmanaged resources are handled correctly.