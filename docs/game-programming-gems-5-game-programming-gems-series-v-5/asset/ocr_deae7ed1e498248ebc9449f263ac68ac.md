![](bbox=[0.215, 0.08, 0.965, 0.375])

FIGURE 1.7.14 Multiple windows, multiple users.

# Optimizing: Multithreaded Paging

An optimization of GP is to avoid the GPworld realizing the calls to the methods Load() and Unload() of the GPtiles immediately. The world will realize these tasks in a separate thread so as to avoid any interference of the load/unload processes with the rest of the system, and thus increase performance.

To do this, the world has a list of GPtiles. When a GPwindow calls to the GPworld for loading (or unloading) a GPtile, the GPworld adds this GPtile to the list and marks it as loadable (or unloadable). In the main loop of the load/unload thread, each element of the list is removed and processed.

# Conclusion

This gem described a complete, multiuser general paging system (GP), capable of managing any type of information in an easy and efficient way, optimizing the resources of the system. The scope of GP is global, so it may be integrated into any other system that requires management of the loading and unloading of information.

The design of the GP follows some of the design suggestions of [Lakos96] and [Alexandrescu01]. The implementation of GP uses some of the suggestions of [Meyers96].

# References

+   [Alexandrescu01] Alexandrescu, Andrei. Modern C++ Design. Addison Wesley, 2001.

+   [Lakos96] Lakos, John. Large-Scale C++ Software Design. Addison Wesley, 1996.

+   [Meyers96] Meyers, Scott. More Effective C++. Addison Wesley, 1996.