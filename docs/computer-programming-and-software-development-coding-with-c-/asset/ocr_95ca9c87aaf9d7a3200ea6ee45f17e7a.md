# Chapter 5 Implicit Typing Fundamentals

Now, I want to briefly discuss one more thing related to types, and it's implicit typing. I have already mentioned a few times that once a type is set for a variable, it's done, it's set, and so far we have been explicit about this, meaning that we included the type name, so int or bool, in its declaration. That is the normal way of doing things in C#.

```
int a = 123;

bool b = true;

double d = 11.0;
```

Since C# 3, so already for quite a few versions, C# supports implicit typing. As the name gives away, implicit typing allows us to ask C# to figure out itself based on what is on the side of the equal sign what the type will be. We use for that the var keyword, basically saying, hey C#, here's a variable, please figure out the type yourself. Take a look here. I have here var a = 123. 123 is an integer value, and thus C# will create a to b of type integer. If we do var b = true, C# will understand that true is a Boolean value and thus b will be of type bool. You may be thinking, is C# then allowing us to omit the type?

```
var a = 123;//a will be an integer
var b = true;//b will be a boolean
var d = 11.0;//d will be a double
```