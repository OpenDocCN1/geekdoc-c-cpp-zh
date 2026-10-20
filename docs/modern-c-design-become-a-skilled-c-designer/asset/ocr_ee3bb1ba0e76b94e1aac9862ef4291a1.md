inline, non-virtual functions compiled in the main application. Finally, exceptions are rarely portable across the binary interface between the main program and plugins, so we cannot throw exceptions in a plugin and try to catch them in the main application.

That was a mouthful. Let’s recap by enumerating the rules for C++ plugins: 1. Memory allocated in a plugin must be deallocated in the same plugin. 2. Standard library components cannot be used in plugin interfaces.

3. Assume incompatible alignment. Avoid plugins inheriting from main application classes with member variables if the variables are used in the main application.

4. Functions exported from a plugin (to be called by the main application) must specify extern "C" linkage. Functions exported from the main application (to be called by plugins) must specify extern "C" linkage.