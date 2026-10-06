# Introduction to Programming and Problem-Solving Using Scala

+   - drawImage(img: Image, x: Double, y: Double, w: Double, h: Double): Draws the specified image into the generic region of the Canvas.

+   - drawImage(img: Image, x: Double, y: Double): Unit - Draws the specified image with the top left corner at the supplied x, y coordinates.

There is also a method called pixelWriter that provides you with a PixelWriter that can be used to write specific pixels directly to the Canvas. Note that you cannot get a PixelReader for the Canvas, if you are writing something that needs to be read pixels, you will need to make a WritableImage and draw to the Canvas using one of the drawImage methods.

# 12.6.5 A Canvas Based Game

We finish this section with an example game that is based entirely on Canvas styles. In the game the player controls a little green dot with the keyboard. Little red dots try to catch the green dot and if they succeed, the player loses. The mouse is used to "draw" puddles on the screen area that slow both the player and the enemies. This is the basic idea.

There are a few more details in the analysis. Puddles evaporate over time to become smaller and enemies only live so long. New enemies pop up at regular intervals. As the game goes, enemies live longer. The real objective is to see how long the player can stay alive. Here is code for this game.

# Listing 12.10: EvadeGame.scala

```
1 import scalaf.includes.
2 import scalaf.application.JFXApp
3 import scalaf.scene.Scene
4 import scalaf.animation.AnimationTimer
5 import scalaf.scene.canvas.
6 import scalaf.scene.control.
7 import scalaf.scene.input.
8 import scalaf.scene.layout.BorderPane
9 import scalaf.scene.paint.Color
10 import scalaf.event.ActionEvent
11
12 class Enemy(x:Double, y:Double, time:Double)
13 class Puddle(x:Double, y:Double, size:Double)
14 class Player(x:Double, y:Double)
15
16 var canvasSize = 600
17
18 var enemies = List[Enemy]()
19 var puddles = List[Puddle](())
20 var player = Player(300,300)
21 var leftPressed = false
22 var rightPressed = false
23 var upPressed = false
24 var downPressed = false
25 var regenDelay = 0.0
```

> There are two methods on Canvas called snapshot that give you a WritableImage that you could read pixels from. However, this approach would be far less efficient than simply making your own WritableImage you can read from, write to, and draw to the GraphicsContext.