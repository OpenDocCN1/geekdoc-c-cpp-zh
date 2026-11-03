
C has been described as like "driving a Porsche with no brakes" - and because it is fast as well this can be exhilarating. C is often the only option when speed and efficiency is crucial.

C has been called "dangerous" in that it allows low-level access to the machine but this scariness is exactly what you need to understand as it gives you respect for the higher-level languages you will use.

Many embedded miniaturised systems are all still written in C and the machine-to-machine world of the invisible internet for monitoring and process control often uses C.

Hopefully this list of reasons will start you to the growing complexity of modern Integrated Development Environments (IDEs) such as Developer Studio, Netbeans and Eclipse which give students an illusion that they know what they are doing but generate obfuscation.

My aim is to get students confident and up to speed quickly without all the nightmare associated with configuring complex tool chains. It is also essentially a license-free approach and runs on anything.

With this fundamental understanding about what is really going on you can progress on to use and actually understand whatever tools you need in your career.

In order to give a sense of doing something real and useful and up to date, the focus is on developing visible and effectively professional-quality web-server and client projects to put on-line, using:

- Apache Web server and development libraries.
- C language CGI programs (C programming using the "make" utility).
- C language Apache modules.
- MySQL server with C client library interfaces.
- GD graphics library with C interfaces.
- Incidental use of CSS, (X)HTML, XML, JavaScript, Ajax.

This course has been designed for and lab-tested by first and second year Computer Science Students at Kingston University, London UK.

## Setting up your System

This book presumes you are using the Linux operating system with either the KDE3.5, KDE4, or Gnome desktop. Specific instructions are included for Ubuntu (and Kubuntu) and OpenSuse 11.

If you are using the KDE desktop you will have Konqueror or Dolphin as the File Manager and kate or kedit for an editor.

In Gnome you would probably use Nautilus and gedit.

You need to be familiar with the idea of doing some things as “super user” so that you have access permission to copy or edit certain files. This is normally done by prefixing the Linux command with “sudo” and providing the password, as in this example:

```
sudo cp hello3 /srv/www/cgi-bin/hello3
```

which copies the file “hello3” to the area where the Apache server locates common gateway interface or cgi programs.

In KDE “kdesu konqueror” would open a file manager as super user.

In Gnome “gnomesu nautilus” would open a file manager as super user.

You will need to have installed the following packages:

| package | Ubuntu | Open Suse |
|---|---|---|
| C development libraries | build-essential | Base Development (pattern) |
| Apache web server | apache2 | Web and LAMP Server (pattern) |
| Apache development libraries | apache2-prefork-dev | apache2-devel |
| MySQL server, client and development libraries | mysql-server libmysqlclient15-dev | libmysqlclient-devel |
| GD and development libraries | libgd2-xpm | gd<br>gd-devel |

Throughout the text you will see references to the folder **cgi-bin**. The location of this will vary between Linux distributions. By default this folder used for web programs is:

- OpenSuse: **/srv/www/cgi-bin**
- Ubuntu: **/usr/lib/cgi-bin**

To place programs there you need superuser rights, so it may be better to create a folder inside your own `home/*****/public_html/cgi-bin` directory and change the **ScriptAlias** and associated **Directory** references inside the Apache configuration files (OpenSuse) `/etc/apache2/default-server.conf` or (Ubuntu) `/etc/apache2/default-server.conf`.

## YOUR CHANCE TO CHANGE THE WORLD

Here at Ericsson we have a deep rooted belief that the innovations we make on a daily basis can have a profound effect on making the world a better place for people, business and society. Join us.

In Germany we are especially looking for graduates as Integration Engineers for

- Radio Access and IP Networks
- IMS and IPTV

We are looking forward to getting your application! To apply and for all current job openings please visit our web page: www.ericsson.com/careers

![](img/a0cbda189e54d8cb1121c7e151992506_11_0.png)

## 1. Chapter One: Hello World

### 1.1 Hello Program 1

Using the File Manager (in KDE, Konqueror or in Gnome, Nautilus) create a new directory somewhere in your home directory called something appropriate for all the examples in this book, perhaps “Programming_In_Linux” without any spaces in the name.

Open an editor (in KDE, kate, or in Gnome, gedit) and type in (or copy from the supplied source code zip bundle) the following:

```
/*
C Programming in Linux (c) David Haskins 2008
chapter1_1.c
*/

#include <stdio.h>

int main(int argc, char *argv[])
{
    printf("Hello, you are learning C!!\n");
    return 0;
}
```

Save the text as chapter1_1.c in the new folder you created in your home directory.

Open a terminal window and type: `gcc -o hello chapter1_1.c` to compile the program into a form that can be executed.

Now type `ls -l` to list the details of all the files in this directory. You should see that chapter1_1.c is there and a file called `hello` which is the compiled C program you have just written.

Now type: `./hello` to execute, or run the program and it should return the text:

"Hello, you are learning C!!"

If this worked, congratulations, you are now a programmer!

### Anatomy of the program:

The part inside `/* ... */` is a comment and is not compiled but just for information and reference.

The `#include` part tells the compiler which system libraries are needed and which header files are being referenced by this program. In our case `printf` is used and this is defined in the stdio.h header.

The `int main(int argc, char *argv[])` part is the start of the actual program. This is an entry-point and most C programs have a main function.

The `int argc` is an argument to the function `main` which is an integer count of the number of character string arguments passed in `char *argv[]` (a list of pointers to character strings) that might be passed at the command line when we run it.

A pointer to something is a name given to a memory address for this kind of data type. We can have a pointer to an integer: `int *iptr`, or a floating point number: `float *fPtr`. Any list of things is described by `[]`, and if we know exactly how big this list is we might declare it as `[200]`. In this case we know that the second argument is a list of pointers to character strings.

Everything else in the curly brackets is the main function and in this case the entire program expressed as lines.

Each line or statement ends with a semi-colon `;`.

We have function calls like `printf(...)` which is a call to the standard input / output library defined in the header file stdio.h.

At the end of the program `return 0` ends the program by returning a zero to the system.

Return values are often used to indicate the success or status should the program not run correctly.

### 1.2 Hello Program 2

Taking this example a stage further, examine the start of the program at the declaration of the entry point function: `int main(int argc, char *argv[])`.

In plain English this means:
