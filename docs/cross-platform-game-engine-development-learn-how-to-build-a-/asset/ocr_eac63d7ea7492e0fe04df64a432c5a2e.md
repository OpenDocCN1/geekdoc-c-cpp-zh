# Core Features

There are some features that are important for almost all C++ project development, whether it is a game engine or not. Things like message logger, assertions, platform-detection, etc. We are going to quickly add those features to our project before moving to the graphics related stuff.

# Message Logger

The message logger is a crucial element for software development in general. This feature will enhance our development experience by talking back to us about our code failures.

Add the code below to the bottom of your precompiled header file pch.h.

```
// ...

#if defined(_DEBUG)
#define FUSE_LOG(level, message, ...) \
    fprintf(stderr, "[%%] ", level); \
    fprintf(stderr, message, ##__VA_ARGS__); \
    fprintf(stderr, "\n");

#define FUSE_WARN NG(message, ...) FUSE_LOG("warning", message,
##__VA_ARGS__)
#define FUSE_ERROR(message, ...) FUSE_LOG("error", message,
##__VA_ARGS__)
#define FUSE_INFO(message, ...) FUSE_LOG("info", message,
##__VA_ARGS__)
#else
#define FUSE_INFO
#define FUSE_ERROR
#define FUSE_WARN G
#endif
```

As you can see if we compile our code with the _DEBUG symbol defined, the macros FUSE_INFO, FUSE_WANING, FUSE_ERROR will also be compiled. But if the _DEBUG symbol is not defined, they won't be compiled. That's something we want because when we are done developing and testing our project, we would want it to only hold what is necessary for the user. We have defined a macro around fprintf().