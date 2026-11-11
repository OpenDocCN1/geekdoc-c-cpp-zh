To decrypt, the class loader simply subtracts the key from every byte. In the companion code for this book, you will find four class files, encrypted with a key value of 3—the traditional choice. To run the encrypted program, you'll need the custom class loader defined in our ClassLoaderTest program.

Encrypting class files has a number of practical uses (provided, of course, that you use something stronger than the Caesar cipher). Without the decryption key, the class files are useless. They can neither be executed by a standard virtual machine nor readily disassembled.

This means that you can use a custom class loader to authenticate the user of the class or to ensure that a program has been paid for before it will be allowed to run. Of course, encryption is only one application of a custom class loader. You can use other types of class loaders to solve other problems—for example, storing class files in a database.

# Listing 10.1 ClassLoader/ClassLoaderTest.java

```
````java
package classLoader;

import java.io.*;
import java.lang.reflect.*;
import java.nio.file.*;
import java.awt.*;
import java.awt.event.*;
import javax.swing.*;

/**
 * This program demonstrates a custom class loader that decrypts class files.
 * @version 1.25 2018-05-01
 * @author Cay Horstmann
 */
public class ClassLoaderTest
{
    public static void main(String[] args)
    {
        EventQueue.invokeLater(() ->
            {
                var frame = new ClassLoaderFrame();
                frame.setTitle("ClassLoaderTest");
                frame.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
                frame.setVisible(true);
            });
    }
}
````
```