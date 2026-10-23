can read and process millions or even billions of values quickly. You now know how to pull this data from files or over networks. You can deal with data in flat text, XML, or binary. You can use higher-order constructs to do the processing and apply multithreading to speed it up.

The also have the ability to write programs that display Graphical User Interfaces (GUIs) and draw custom graphics. You can write programs that talk to one another over networked sockets. When it really comes down to it, you have learned the basic tools to make a computer do pretty much anything. You have the foundation to create any application you can dream up.

# 36.2 The Possibilities/A Pet Project

So where should you go from here? Remember that programming is an art. You gain skill primarily by applying that art. If you do not apply it, you will lose your skill. As such, you need to exercise this art. There are many ways you can do this. The most important thing for you to do though is to pick a project. It does not have to be a really big project. If it is small, when you complete it you will simply pick another one. However, having a project outside of your normal course work gives you a great way to further develop your skills. It also allows you to build a portfolio of your work.

When you pick a project, you will need to look into what it takes to do it. Not all projects will favor you working in Scala. That is not a problem. Learning another language is a great exercise. It is always easier to learn the second than it was to learn the first and having knowledge of multiple languages often helps you to see problems from different perspectives. There are many types of projects that you can do in Scala though. Consider these possibilities.

# 36.2.1 General 2-D Application

What you know how to do best at this point is write applications. If you can think of something that interests you that works as an application, run with it. Whether it is something useful or just something for fun, there are vast possibilities in what you can get a computer to do. Take advantage of your ability to do graphics and GUIs. Make something networked or push the parallelism to fully utilize newer hardware.

# 36.2.2 3-D Application

If you are playing with graphics, you might want to do something in 3-D. You can render things in 3-D with ray tracing or other techniques that work in 2-D. However, if you are willing to do a bit of extra reading, which you should be, you can use Scala to write full 3-D applications through some different Java libraries.

The most standard 3-D graphics library is OpenGL®. There are several Java-based wrappers for OpenGL. The most established of these is called JOGL, the Java bindings for OpenGL. OpenGL takes advantage of 3-D hardware to make 3-D rendering fast.

The primary downfall of OpenGL is that it is a low-level API. That means you are setting up geometry and giving instructions to render it in a way that is close to what the machine wants. There are also higher level libraries like Java3D®. These use scene graph representations and can often be easier to use when you want to get things up and running.