```
0; virtual PluginCommand*
clonePluginImpl() const noexcept = 0;

void checkPreconditionsImpl() const
overridefinal;
PluginCommand* cloneImpl() const
overridefinal;
};
```

While only mentioned briefly in Chapter 4, all of the pure virtual functions in theCommand class are markednoexcept except for checkPreconditionsImpl() and cloneImpl() (see the sidebar on keyword noexcept). Therefore, to ensure that plugin commands do not originate exceptions, we simply implement the checkPreconditionsImpl() and cloneImpl() functions at the PluginCommand level of the hierarchy and create new, exception-free, pure virtual functions for its derived classes to implement. checkPreconditionsImpl() and cloneImpl() are both marked final in the PluginCommand class to prevent specializations from inadvertently overriding either of these functions. The implementation