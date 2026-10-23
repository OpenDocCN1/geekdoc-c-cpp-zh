# Chapter 12

# Graphics

+   12.1 Custom-Drawn Panels ................................................... 284
+   12.2 java.awt.Graphics2D ................................................... 284
+   12.2.1 Shapes .............................................................. 285
+   12.2.2 Settings ............................................................. 287
+   12.2.2.1 Paint ............................................................. 287
+   12.2.2.2 Stroke ............................................................ 290
+   12.2.2.3 Font .............................................................. 292
+   12.2.2.4 Clip .............................................................. 294
+   12.2.2.5 Transform ....................................................... 294
+   12.2.3 Affine Transforms .................................................. 294
+   12.3 Images ............................................................... 297
+   12.3.1 BufferedImage ...................................................... 297
+   12.3.2 Reading and Writing Images ....................................... 298
+   12.3.3 Double Buffering .................................................. 298
+   12.3.4 Revisiting TexturePaint ........................................... 299
+   12.4 Other Events ........................................................ 299
+   12.4.1 Mouse Events ...................................................... 301
+   12.4.2 Keyboard Events ................................................... 302
+   12.5 Animation with Timer ............................................... 303
+   12.6 Putting it Together ................................................ 304
+   12.7 End of Chapter Material ............................................ 307
+   12.7.1 Summary of Concepts .............................................. 307
+   12.7.2 Exercises ......................................................... 309
+   12.7.3 Projects .......................................................... 309

Not everything that you might ever want to put into a Graphical User Interface (GUI) is part of the standard GUI library. They have only added elements that are used fairly frequently. There are also times when you want to display your own graphics, something completely unique to your program, in a GUI. In order to do this, you have to be able to write graphics code.

Scala does not have its own graphics library. This is because the one in Java is quite complete and works well in a Scala style. The graphics capabilities of Java we will be using are collectively referred to as Java2D because they are the 2-D graphics libraries in Java. The types that we will use are primarily located in three different packages: java.awt, java.awt.geom, and java.awt.image.