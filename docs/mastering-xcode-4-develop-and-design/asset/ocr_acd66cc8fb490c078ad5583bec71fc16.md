![](bbox=[0.067, 0.171, 0.863, 0.293])

# FIGURE 14.13

A per-configuration setting

You can also have per-configuration settings. That is, separate settings for Debug versus Release configurations (or any others you define). In **Figure 14.13**, you see that the Strip Debug Symbols During Copy setting has an open disclosure triangle next to it and has separate settings for the two configurations—Debug and Release. It would be pointless to remove debugging information from a debug build, so the build system will strip debug symbols only from a release build, leaving them intact for debug builds. This is an excellent example of why different configurations (or at least separate settings for debug and release) are necessary. The information is removed from a release version to reduce the size of the executable and to improve performance.

> **NOTE:** The disclosure control appears only for settings that already have per-configuration values defined.