reference to a Transform might be named `_TR`. A variable used to talk to a Game Manager might be named `_GameManager`.

Most of the objects in this book (players, enemies, and more) derive from the ExtendedMonoBehaviour class, which contains a few variables that are used more commonly than others:

+   - `_RB` — Used to reference a Rigidbody attached to this object.
+   - `_RB2D` — For a 2D Rigidbody reference.
+   - `_TR` — The Transform of the object.
+   - `_GO` — The GameObject.

Where scripts need to be initialized before they can be used, in this book we always use a Boolean variable named `didInit` which gets set to true after initialization. You can use `didInit` to make sure initialization has completed.

Many programmers frown on the idea of declaring temporary variables, but I like to have `_tempVEC` and `_tempTR` variables available for whenever I need to refer to a quick Vector3 or another Transform inline. Having these variables already declared is just a little quicker than having to declare a new Vector3 each time, or to make a new Transform variable.

# 1.3 Where to Now?

Think about how your objects work together in the game world and how their scripts need to communicate with each other. I find it helps to make flow diagrams or to use mind-mapping software to work things out beforehand. A little planning early on can reduce a whole lot of code revisions later. That said, it is perfectly O.K. for your structure to grow and evolve as you develop it further. The framework shown in this book went through many iterations before reaching its final form.

Try to break up your scripts into smaller components to help debugging and flexibility. Also try to design for re-usability; hard-coding references to other scripts reduces the portability of the script and increases the amount of work you will need to do in the future when you want to carry it over into another project.