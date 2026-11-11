# Listing 11.22  *(Continued)*

```
```java
private BufferedImage image;

public ImageProcessingFrame()
{
   setTitle("ImageProcessingTest");
   setSize(DEFAULT_WIDTH, DEFAULT_HEIGHT);

   add(new JComponent()
      {
         public void paintComponent(Graphics g)
         {
            if (image != null) g.drawImage(image, 0, 0, null);
         }
      });

   var fileMenu = new JMenu("File");
   var openItem = new JMenuItem("Open");
   openItem.addActionListener(event -> openFile());
   fileMenu.add(openItem);

   var exitItem = new JMenuItem("Exit");
   exitItem.addActionListener(event -> System.exit(0));
   fileMenu.add(exitItem);

   var editMenu = new JMenu("Edit");
   var blurItem = new JMenuItem("Blur");
   blurItem.addActionListener(event ->
      {
         float weight = 1. / 9.0f;
         float[] elements = new float[9];
         for (int i = 0; i < 9; i++)
            elements[i] = weight;
         convolve(elements);
      });
   editMenu.add(blurItem);

   var sharpenItem = new JMenuItem("Sharpen");
   sharpenItem.addActionListener(event ->
      {
         float[] elements = { 0.0f, -1.0f, 0.0f, -1.0f, 5.f, -1.0f, 0.0f, -1.0f, 0.0f };
         convolve(elements);
      });
   editMenu.add(sharpenItem);
```
```