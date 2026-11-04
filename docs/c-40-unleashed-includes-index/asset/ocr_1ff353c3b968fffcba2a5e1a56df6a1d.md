provide efficient call site code generation so that subsequent calls do not suffer from overload resolution again. If overload resolution fails, a runtime exception results.

# DYNAMIC = VAR

Do not confuse the dynamic keyword with the var keyword from C# 3.0. The var keyword is as statically typed as it possibly can; it just enables you to omit the type and let the compiler infer it for you:

```
var languages = new List<ProgrammingLanguage>();
```

The preceding line means exactly the same as the much more verbose variant:

```
List<ProgrammingLanguage> languages = new List<ProgrammingLanguage>();
```

Trying to call a nonexistent method on the languages variable, say the misspelled Add method, will result in a compile-time error. Or even better, the Visual Studio editor will catch the error immediately because all static type information is readily available.

In contrast, with the dynamic keyword, you’re essentially telling the compiler not to bother attempting to infer the type, having it do overload resolution at runtime instead.

A more detailed explanation about how the C# compiler emits code that causes the DLR to kick in—allowing it to reach out to any kind of dynamically typed code—will follow in Chapter 22, “Dynamic Programming.”

# STATIC WHEN POSSIBLE, DYNAMIC WHEN NECESSARY

The introduction of dynamic doesn’t mean you should start rewriting all your statically typed code to use dynamically typed code instead. Static typing has many advantages, and C# stays faithful to that belief. So whenever possible, use static typing—it’s pure goodness.

But other than before the introduction of C# 4.0, when you absolutely need to go for dynamic typing, it’s no longer a mission impossible to get it to work while keeping the code readable and maintainable. What the new dynamic feature really enables is to “gradually ease into” dynamic domains without sacrificing developer productivity.

By the way, if you don’t like dynamic at all and you want to keep people from using the feature, I have good news. It’s relatively straightforward to disable dynamic support simply by emitting the “C# binder” during compilation (which can be achieved through the Visual Studio 2010 IDE, for instance). I’ll get back to that later when we cover dynamic end to end.

# What the DLR Has to Offer

Execution of dynamically typed code relies on quite a few runtime services, such as overload resolution, code generation, and caching of acquired runtime data, to improve efficiency of calls. Let’s explore what’s involved in making a dynamic call.

First, the language compiler generates code to package up all the information it has about the intended call. This includes the type and name of the operation being invoked—for