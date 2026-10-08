private on your classes. Doing this allows you to guarantee that your object always remains in a consistent state. In addition it allows you to change your mind in the future about the implementation details (i.e., how data is stored) without users of your class being affected in anyway.

In summary, the private keyword allows you to perform more sophisticated information hiding than just choosing what to put in the header file.

Not putting a class in a header file gives even more information hiding than making things private, so that should always be your first choice. However, if you have to make the class available to users of your library, you should try to make all its data, and as many of its member functions as possible, private.

It was only for the sake of simplicity that we have given the BlackScholes-Model and the CallOption public data members. We wanted to illustrate the use of public data before explaining about private data. In practice the library could be improved by modifying these classes.

The idea of hiding data using the private keyword is often called encapsulation. The word encapsulation really refers to two things:

+   (i) the bundling together of related items into a single object;

+   (ii) preventing direct messing with the internal data of an object.

Encapsulation is common in real-world design as well as in object-oriented software design. For example, consider the design of a car.

In a car, all the lighting controls are put on the dashboard and are clearly separated from the controls for the windows and the seats. This grouping of functionality in a car's controls corresponds to the grouping of functionality into different classes in software design.

In addition, you can control a car through standard functions (turn left, turn right, etc.) but the internal workings of a car are hidden from the user completely (they're kept under the bonnet). This corresponds to the software design principle of having a small number of public functions that are available to your users, but keeping most of the details private.

Cars are much easier to use because of the use of encapsulation. It is a good thing that you can drive a car without being a trained mechanic. Just as these design principles make cars easier to use, so the same principles make objects in object-oriented programs easy to use.

To illustrate this further, consider the question of how the vector<double> class stores its data given that it can't be using a vector<double> itself. You don't know how this is done, and quite reasonably you probably don't care that much. You don't need to know and your life has been made easier by not having to think about this.

The designer of the C++ libraries has tried to make life easier for you by making the internal data of a vector private. You should help users of your library in the same way.