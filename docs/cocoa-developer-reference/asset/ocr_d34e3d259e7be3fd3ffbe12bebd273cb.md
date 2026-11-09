| Layer | Elements | Components |
|---|---|---|
| Graphics and Media | Core Animation<br>Core Image<br>Core Video<br>QuickTime<br>OpenGL<br>Quartz<br>Core Audio | These elements include still image, animation, and video and audio support. This list is a shortened summary, and the names listed here don’t map exactly to the names of the frameworks that implement these features. But these names are often used as generic descriptions for groups of related libraries. |
| Data and Data Management | Core Data<br>Address Book<br>Calendar | Use these elements to manage data within an application and to exchange data with Apple’s own built-in applications. The Apple frameworks have their own separate internal data management features. Many applications use both kinds of data management. |
| Darwin, Kernel and Driver | UNIX system calls<br>Driver libraries | OS X is built on the BSD (Berkeley Software Distribution) variant of UNIX and includes all the usual low-level UNIX system calls. This level handles direct — high risk — access to hardware features, such as disk hardware or the temperature sensor. It also handles calls to the underlying Darwin version of the UNIX OS. |

Figure 2.2 shows how these elements are related to each other graphically. The most sophisticated and abstract layers are at the top of the diagram. As you travel away from the User Experience layer, you move into the internals of OS X, eventually reaching the underlying UNIX code.

**Figure 2.2**

This simplified functional view is useful to orient you, but a code-level view of frameworks and layers is more relevant in practice.

![](bbox=[0.186, 0.647, 0.401, 0.811])

# Cocoa, Aqua, and the user experience

Aqua is a key part of the user experience. While Cocoa is a code library, Aqua is a look and feel, defined in part by the glass-like interface graphics pioneered by Apple. As a developer, you don’t program an Aqua layer, and there is no Aqua framework. Instead, the visible parts of Aqua are implemented for you automatically. Whenever you add a standard button graphic to your