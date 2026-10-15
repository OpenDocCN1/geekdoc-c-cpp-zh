# Chapter 8 Importing Namespaces

This class belongs to this namespace, and this class belongs to this other namespace. If they were in the same namespace they would see each other, but they're not, so we cannot just use the short name, WeatherUtilities here. We have to use its fully qualified name, like this. And now the error went away.

![](bbox=[0.121, 0.337, 0.838, 0.484])

We have another error now, but the previous one about not being able to see the class, that one's fixed. On the other hand, in C# you use class names all the time, and you probably don't want to use qualified class names all the time. That would make the code really verbose. Instead, you can write something like this at the top of your file. This using directive means, whenever I use this name WeatherUtilities in this file, what I actually mean is this qualified name.

![](bbox=[0.121, 0.746, 0.913, 0.834])

Essentially, this is an alias for this, and now I can use the alias instead of the fully qualified name. And we can make it even shorter.