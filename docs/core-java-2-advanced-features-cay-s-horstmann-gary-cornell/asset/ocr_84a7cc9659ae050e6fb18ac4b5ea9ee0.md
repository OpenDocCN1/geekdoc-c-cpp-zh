If your application is ready to go as soon as it reaches `main`, you can skip the remainder of this section. However, many applications use a plugin architecture in which a small core loads a set of plugins at startup. Eclipse and NetBeans are typical examples. In that case, you can indicate the loading progress on the splash screen.

There are two approaches. You can draw directly on the splash screen, or you can replace it with a borderless frame with identical contents and then draw inside the frame. Our sample program shows both techniques.

To draw directly on the splash screen, get a reference to the splash screen and get its graphics context and dimensions:

```
SplashScreen splash = SplashScreen.getSplashScreen();
Graphics2D g2 = splash.createGraphics();
Rectangle bounds = splash.getBounds();
```

You can now draw in the usual way. When you are done, call `update` to ensure that the drawing is refreshed. Our sample program draws a simple progress bar, as seen in the left image in Figure 11.47.

```
g.fillRect(x, y, width * percent / 100, height);
splash.update();
```

![](bbox=[0.34, 0.525, 0.747, 0.881])

**Figure 11.47** The initial splash screen and a borderless follow-up window