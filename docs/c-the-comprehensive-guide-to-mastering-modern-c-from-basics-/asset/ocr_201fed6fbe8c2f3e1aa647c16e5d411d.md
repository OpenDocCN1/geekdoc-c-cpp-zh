operations. In that case, the compiler generates the move operations for you.

Or the compiler prohibits moving, similar to how it would prohibit copying. For example, if you have a const data field, it cannot be moved from.

If you manage to create a movable data type, it is ideal for return values and for being put into standard containers. The compiler ensures that sorting, swapping, pushing, and resizing use the move operations. The noble goal of a data type is to be put into a container is to be movable. You can achieve this in two ways:

+   - Give your class only data fields that are themselves movable—example, built-in types, standard containers, or types from the standard library.

+   - You take on the thankless task of implementing the move operations yourself.

You should not do the latter, really. And if you do, then let me tell you you must also write noexcept after those operations—such a profound topic that I have touched on it in this book (see Chapter 7).

| 16.9.1 | What the Compiler Generates |

It is important to understand when the compiler takes over the work of generating a constructor or operator= for programmers and when it does not. The rules are not trivial, but they are written in such a way that your program becomes as safe and fast as possible automatically.