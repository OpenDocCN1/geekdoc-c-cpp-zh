# ## 12.12 **Logging**

One common task when handling exceptions is to log where they occurred into a human-readable text file that developers can analyze later for debugging purposes. Logging can be used during development time to help locate and fix problems. It also can be used once an application ships—in if an application crashes, it might write a log file that the user can then send to the developer.

Logging is not built into the C++ standard library, though you could create your own logging mechanisms using C++’s file-processing capabilities. However, there are many open-source C++ logging libraries:

+   - Boost.Log—https://www.boost.org/doc/libs/1_75_0/libs/log/doc/html/
+   - Easylogging++—https://github.com/amrayn/easyloggingpp.
+   - Google Logging Library (glog)—https://github.com/google/glog.
+   - Loguru—https://github.com/emilk/loguru.
+   - Plog—https://github.com/SergiusTheBest/plog.
+   - spdlog—https://github.com/gabime/spdlog.

Some of these are header-only libraries that you can simply include in your projects. Others require installation procedures.

# ### Checkpoint

*(Fill-in)* Logging is built into the C++ standard library.

**Answer:** False. Actually, logging is not built into the C++ standard library, though you could create your own logging mechanisms using C++’s file-processing capabilities. There are many open-source C++ logging libraries.

# ## 12.13 **Looking Ahead to Contracts**⁴⁹

To strengthen your program’s error-handling architecture, you can specify the expected states before and after a function’s execution with preconditions and postconditions, respectively. We’ll define each, show precodition code examples and explain what happens when contracts are violated:

+   - A description⁵⁰ must be true when a function is invoked. Preconditions describe constraints on function parameters and any other expectations the function has just before it begins executing. If the preconditions are not met, then the function’s behavior is undefined—it may throw an exception, proceed with an illegal value or attempt to recover from the error. If code with undefined behavior is allowed to proceed, the results could be unpredictable and not portable across platforms. Each function can have multiple preconditions.

49. **Contracts are not yet a standard C++ feature.** The syntax we show here could change.

50. “Precondition.” Wikipedia. Wikimedia Foundation. Accessed April 18, 2023. https://en.wikipedia.org/wiki/Precondition.