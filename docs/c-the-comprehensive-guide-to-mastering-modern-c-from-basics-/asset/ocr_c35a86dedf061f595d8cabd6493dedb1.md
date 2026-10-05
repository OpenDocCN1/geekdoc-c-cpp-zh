# ## 2.5 The Command Line under Ubuntu

As an example for the development with the command line, I will give you a quick guide for the current long-term version of Ubuntu, a widely used Linux distribution. If you are using a different Linux distribution, the commands may differ.

You install g++ and some useful tools like this:

```
sudo apt-get install g++ make
```

You enter the program code in an editor, and this is where the real agony of choice begins. If you are using an IDE, the editor is included. Without an IDE, you enter your program in any general text editor. Text editors are a dime a dozen.

I am only suggesting two that meet different requirements: gedit and kate. The choice between gedit and kate should depend on whether you are using Gnome or KDE as your desktop. Simply try out which of the following two commands would install fewer packages automatically, and then select the editor:

```
sudo apt-get install gedit
sudo apt-get install kate
```