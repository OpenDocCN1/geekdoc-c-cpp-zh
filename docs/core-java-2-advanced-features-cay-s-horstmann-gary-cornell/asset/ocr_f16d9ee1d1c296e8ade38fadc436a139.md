![](bbox=[0.219, 0.141, 0.696, 0.323])

Figure 5.6  The ViewDB application

# Listing 5.4  `view/ViewDB.java`

```
package view;

import java.awt.*;
import java.awt.event.*;
import java.io.*;
import java.nio.file.*;
import java.sql.*;
import java.util.*;

import javax.sql.*;
import javax.sql.rowset.*;
import javax.swing.*;

/**
 * This program uses metadata to display arbitrary tables in a database.
 * @version 1.33 2016-04-27
 * @author Cay Horstmann
 */
public class ViewDB
{
   public static void main(String[] args)
   {
      EventQueue.invokeLater(() ->
         {
            JFrame frame = new ViewDBFrame();
            frame.setTitle("ViewDB");
            frame.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
            frame.setVisible(true);
         });
   }
}
```