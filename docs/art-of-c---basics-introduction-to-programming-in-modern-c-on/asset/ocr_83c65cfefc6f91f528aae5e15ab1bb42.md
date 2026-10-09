**key-value-store/Common/IServer.cs (lines 3-10)**

```
public interface IServer<T> {
 string? Ping();
 T? Get(string key);
 T? Set(string key, T value);
 string[] Keys();
 bool Exists(string key);
 T? Del(string key);
}
```

# ### Author’s Note

# ## Request for Feedback

The author is always looking to improve the book.

If you have any suggestions, then please let us know. We, and the future readers, will really appreciate it.

It can be anything from simple typos, unclear sentences, and formatting errors to any bugs in the sample code and maybe downright incorrect explanations. Here’s the author’s email:

+   - harry@codingbookspress.com.

The author will try to correct the errors as soon as possible, as needed.

Thank you!