| Example | Description |
|---|---|
| Clock | Draws a clock with rotating hands, the current date and the current time. The clock updates once per second. |
| DitherTest | Demonstrates drawing with a graphics technique known as dithering that allows gradual transformation from one color to another. |
| DrawTest | Allows the user to draw lines and points in different colors by dragging the mouse. |
| Fractal | Draws a fractal. Fractals typically require complex calculations to determine how they're displayed. We discuss fractals in Section 18.8. |
| GraphicsTest | Draws shapes to illustrate graphics capabilities. |
| GraphLayout | Draws a graph consisting of many nodes (represented as rectangles) connected by lines. Drag a node to see the other nodes in the graph adjust on the screen and demonstrate complex graphical interactions. |
| JumpingBox | Moves a rectangle randomly around the screen. Try to catch it by clicking it with the mouse! |
| MoleculeViewer | Presents a three-dimensional view of several chemical molecules. Drag the mouse to view the molecule from different angles. |
| NervousText | Draws text that jumps around the applet. |
| SimpleGraph | Draws a complex curve. |
| SortDemo | Compares three sorting techniques. Sorting (described in Chapter 19) arranges information in order—like alphabetizing words. When you execute this example with the appletviewer, three windows appear. When you execute it in a browser, the three demos appear side by side. Click in each demo to start the sort. The sorts all operate at different speeds. |
| SpreadSheet | Demonstrates a simple spreadsheet of rows and columns. |
| TicTacToe | Allows the user to play Tic-Tac-Toe against the computer. |
| WireFrame | Draws a three-dimensional shape as a wire frame. Drag the mouse to view the shape from different angles. |

Fig. 23.1 | The examples from the applets directory. (Part 2 of 2.)

# TicTacToe Applet

This TicTacToe demonstration applet allows you to play Tic-Tac-Toe against the computer. Change directories to subdirectory TicTacToe, where you'll find the file example1.html that loads the applet. In the command window, type the command

```
appletviewer example1.html
```

and press Enter. This executes the appletviewer applet container, which loads the HTML document example1.html specified as its command-line argument. The appletviewer determines from the document which applet to load and executes it. Figure 23.2 shows several screen captures of playing Tic-Tac-Toe with this applet. You can open the HTML document in your browser to execute the applet in the browser.

You are player X. To interact with the applet, point the mouse at the square where you want to place an X and click the mouse button. The applet plays a sound and places an X