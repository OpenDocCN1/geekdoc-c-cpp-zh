![](bbox=[0.324, 0.141, 0.763, 0.309])

**Figure 11.3** Resizing columns

you should either make cells uneditable or handle cell editing events and update your model. We will discuss those topics later in this section.

Finally, click on a column header. The rows are automatically sorted. Click again, and the sort order is reversed. This behavior is activated by the call

```
table.setAutoCreateRowSorter(true);
```

You can print a table with the call

```
table.print();
```

> > **CAUTION:** If you don't wrap a table into a scroll pane, you need to explicitly add the header:
> >
> > ```java
> > add(table.getTableHeader(), BorderLayout.NORTH);
> > ```

# **Listing 11.1** `table/TableTest.java`

```
package table;

import java.awt.*;
import java.awt.print.*;

import javax.swing.*;

/**
 * This program demonstrates how to show a simple table.
 * @version 1.14 2015-05-01
 * @author Cay Horstmann
 */
```