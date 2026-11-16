# ## Automatic Memory Management

Lua manages memory automatically. When a value is no longer referenced, it is made available for garbage collection. Thus, there is no need to specifically free any memory. Keep in mind, though, that holding references to unneeded objects will prevent them from being cleaned up.

# ## The Lua State

There are a few Lua terms that warrant quick definitions, and the first is the Lua _state_. Essentially, a Lua state is a single operating environment for the Lua interpreter including the stack, execution state, global variables, and so forth. The Lua state is the object with which we interface when embedding the language into a game. Most architectures will need only one Lua state.

# ## Lua Chunks

A _chunk_ is a sequence of statements that are translated, and optionally executed, by Lua. Chunks can be thought of as programs, or fragments of programs, that are loaded into the Lua environment and made available for use. Chunks usually come from files in the form of scripts but can also come from static text strings within another chunk, or even directly from a command console. In the latter case, a chunk can be a single statement typed in by the user.

# ## Interfacing Lua with C

From a game programmer's point of view, one of the most attractive aspects of Lua is how simply it interfaces with C. Before examining how to actually embed Lua and feed it with scripts, we will explore how to make C functions available to the interpreter.

Communication between the two languages is provided via a stack, which serves both as an insulation layer as well as a translation mechanism. Because Lua is dynamically typed, a single stack entry can represent data of any Lua type, so translation routines are provided to get the data into a format usable by C.

# ## Calling C Code from Lua

The first task most programmers want to accomplish is to expose some functionality of their game engine to Lua and make it available for script-based control. This is done by registering simple "glue" routines with Lua. Say we want a Lua script to be able to control where our in-game camera is looking. We want the Lua script to look something like this:

```
- Point the camera at the volcano
Camera.SetTargetPos(100.0, 40.0, 230.0);
```