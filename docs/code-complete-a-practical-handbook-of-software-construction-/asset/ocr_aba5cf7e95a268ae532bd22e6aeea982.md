Notice that the *Coordinate* type is declared as *private* in the package specification. That means that the only part of the program that knows the definition of the *Coordinate* type is the private part of the *Transformation* package. In a development environment with a group of programmers, you could distribute only the package specification, which would make it harder for a programmer working on another package to look up the underlying type of *Coordinate*. The information would be literally hidden. Languages like C++ that require you to distribute the definition of *Coordinate* in header files undermine true information hiding.

These examples have illustrated several reasons to create your own types:

+   - **To make modifications easier**  It’s little work to create a new type, and it gives you a lot of flexibility.
+   - **To avoid excessive information distribution**  Hard typing spreads data-typing details around your program instead of centralizing them in one place. This is an example of the information-hiding principle of centralization discussed in Section 6.2.
+   - **To increase reliability**  In Ada, you can define types such as *type Age is range 0..99*. The compiler then generates run-time checks to verify that any variable of type Age is always within the range 0..99.
+   - **To make up for language weaknesses**  If your language doesn’t have the pre-defined type you want, you can create it yourself. For example, C doesn’t have a boolean or logical type. This deficiency is easy to compensate for by creating the type yourself:
+   
+     ```c
+     typedef int Boolean;
+     ```

# Why Are the Examples of Creating Your Own Types in Pascal and Ada?

Pascal and Ada have gone the way of the stegosaurus and, in general, the languages that have replaced them are more usable. In the area of simple type definitions, however, I think C++, Java, and Visual Basic represent a case of three steps forward and one step back. An Ada declaration like

```
currentTemperature: INTEGER range 0..212;
```

contains important semantic information that a statement like

```
int temperature;
```

does not. Going a step further, a type declaration like

```
type Temperature is range 0..212;
...
currentTemperature: Temperature;
```