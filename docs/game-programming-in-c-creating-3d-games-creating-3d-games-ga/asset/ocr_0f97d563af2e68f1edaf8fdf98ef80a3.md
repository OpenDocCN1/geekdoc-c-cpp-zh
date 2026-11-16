The header `fmod_studio.hpp` defines the FMOD Studio API types. However, to avoid this include, `AudioSystem.h` instead creates forward declarations of the FMOD types. This way, you only need to include the FMOD header in `AudioSystem.cpp`.

Initializing FMOD, which is handled in `AudioSystem::Initialize`, involves several steps. First, call `Debug_Initialize` to set up error logging:

Click here to view code image

```
FMOD::Debug_Initialize(
    FMOD_DEBUG_LEVEL_ERROR, // Log only errors
    FMOD_DEBUG_MODE_TTY // Output to stdout
);
```

The first parameter to `Debug_Initialize` controls the verbosity of the logging messages. (The default is quite verbose.) The second parameter specifies where to write log messages. In this case, log messages write to `stdout`. For games that have custom debug code, it's also possible to declare a custom callback function for all FMOD log messages.

**note**

Initializing debug logging is relevant only if you're using the logging build of FMOD, as is the case in this chapter. Enabling error logging is extremely useful during development, but a shipped version of a game shouldn't include logging.