```
```csharp
public const int NORTHWEST = 7;
public const int WEST = 8;

// Member data
public int imageWidth; // Width of the image
public int imageHeight; // Height of the image
public int imagePosX; // X Position in containing object
public int imagePosY; // Y Position in containing object
public Image imageData; // The image itself

public int imageOffsetX; // facilitates "relative" positioning
public int imageOffsetY; // by placing image at a specified
// offset to PosX, PosY.

public int animationStep; // How much the image should move/step

public Rectangle constraintBox; // Our sandbox to play in
public int direction; // current direction the image is heading
public bool isActive; // whether the image should be animated
public AnimatedImage owner; // if it's controlled by another image

#region Constructors
public AnimatedImage() : this(0,0) {} // default constructor

public AnimatedImage(int posX, int posY) {
imagePosX = posX;
imagePosY = posY;
isActive = false;
animationStep = DEFAULTSTEP;
}
#endregion
...
```
```

![](bbox=[0.1, 0.78, 0.22, 0.88])

> Remember, C# class references aren't part of the main program, so they do not require a main method. Also, it's important to note that the class is left open-ended, so as to include our methods, which are discussed over the next few sections.