However, for the compiler to process this statement, it needs to have already seen the Remote definition. Otherwise, it won’t know that Remote is a class and that set_chan() is a method of that class. This suggests putting the Remote definition above the Tv definition. But the fact that Remote methods mention Tv objects means that the Tv definition should appear above the Remote definition. Part of the way around the circular dependence is to use a forward declaration. To do so, you insert the following statement above the Remote definition:

```
class Tv;            // forward declaration
```

This provides the following arrangement:

```
class Tv; // forward declaration
class Remote { ... };
class Tv { ... };
```

Could you use the following arrangement instead?

```
class Remote;        // forward declaration
class Tv { ... };
class Remote { ... };
```

The answer is no. The reason, as mentioned earlier, is that when the compiler sees that a Remote method is declared as a friend in the Tv class declaration, the compiler needs to have already viewed the declaration of the Remote class in general and of the set_chan() method in particular.

Another difficulty remains. In Listing 15.1, the Remote declaration contains inline code such as the following:

```
void onoff(Tv & t) { t.onoff(); }
```

Because this calls a Tv method, the compiler needs to have seen the Tv class declaration at this point so that it knows what methods Tv has. But as you’ve seen, that declaration necessarily follows the Remote declaration. The solution to this problem is to restrict Remote to method declarations and to place the actual definitions after the Tv class. This leads to the following ordering:

```
class Tv;            // forward declaration
class Remote { ... };   // Tv-using methods as prototypes only
class Tv { ... };
// put Remote method definitions here
```