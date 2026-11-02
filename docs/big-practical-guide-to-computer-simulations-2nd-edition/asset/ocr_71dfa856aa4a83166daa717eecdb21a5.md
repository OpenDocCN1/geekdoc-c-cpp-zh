![](bbox=[0.25, 0.18, 0.8, 0.62])

Fig. 5.1 An example for objects. There are objects of different type, here "atoms", "containers" and solvent "water". Each object has internal states or variables and interacts with the other objects via defined access interfaces. For example, in a simulation of proteins dissolved in water, an atom has a position and a velocity, which are influenced via forces from other atoms, the solvent and the container.

the object-oriented and the procedural world, depending on the actual problem. In modern programming, usually only the basic functionality is implemented as methods, while many algorithms are implemented via standard subroutines.

+   - **Data capsuling**

When using a computer, you do not care about the implementation. When you press a key on the keyboard, you would like to see the result on the screen. You are not interested in how the key converts your keystroke into an electrical signal, how this signal is sent to the input ports of the chips, how the algorithm treats the signal and so on. Similarly, a main principle of object-oriented programming is to hide the actual implementation of the objects. Access to them is only allowed via given interfaces, i.e. via methods. The internal data structures are hidden, this is called **private** in C++. The data capsuling has several advantages:

+   - You do not have to remember the implementation of your objects.

When using them later on, they just appear as a black box fulfilling