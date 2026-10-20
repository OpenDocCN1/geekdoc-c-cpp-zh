managing the lifetime of plugins, or injecting plugin functionality into pdCalc. These operations are performed by aPluginLoader class and themain() function of the application, both of which are now described.

# 7.5.1 Loading Plugins

Loading plugins is accomplished by a PluginLoader class. The PluginLoader is responsible for finding plugin dynamic library files, loading the plugins into memory, and serving the concrete Plugin specializations to pdCalc, on demand. The PluginLoader is also responsible for deallocating plugin resources at the appropriate times. As we’ve seen previously, a good design will implement automatic deallocation via RAII.

The first step in loading plugins is determining which plugins should be loaded and when. Really, only two practical options exist to answer this question. Either plugins are loaded automatically by pdCalc when the program starts (e.g., files specified in a