# **Listing 11.7** *(Continued)*

```
```java
68   String name = f.getName();
69   String suffix = name.substring(name.lastIndexOf('.') + 1);
70   Iterator<ImageReader> iter = ImageIO.getImageReadersBySuffix(suffix);
71   ImageReader reader = iter.next();
72   ImageInputStream imageIn = ImageIO.createImageInputStream(f);
73   reader.setInput(imageIn);
74   int count = reader.getNumImages(true);
75   images = new BufferedImage[count];
76   for (int i = 0; i < count; i++)
77   {
78      images[i] = reader.read(i);
79      box.add(new JLabel(new ImageIcon(images[i])));
80   }
81   }
82   catch (IOException e)
83   {
84      JOptionPane.showMessageDialog(this, e);
85   }
86   setContentPane(new JScrollPane(box));
87   validate();
88   }
89
90   /**
91    * Save the current image in a file.
92    * @param formatName the file format
93    */
94   public void saveFile(final String formatName)
95   {
96      if (images == null) return;
97      Iterator<ImageWriter> iter = ImageIO.getImageWritersByFormatName(formatName);
98      ImageWriter writer = iter.next();
99      JFileChooser chooser = new JFileChooser();
100     chooser.setCurrentDirectory(new File("."));
101     String[] extensions = writer.getOriginatingProvider().getFileSuffixes();
102     chooser.setFileFilter(new FileNameExtensionFilter("Image files", extensions));
103
104     int r = chooser.showSaveDialog(this);
105     if (r != JFileChooser.APPROVE_OPTION) return;
106     File f = chooser.getSelectedFile();
107     try
108     {
109        ImageOutputStream imageOut = ImageIO.createImageOutputStream(f);
110        writer.setOutput(imageOut);
111
112        writer.write(new IIOImage(images[0], null, null));
113        for (int i = 1; i < images.length; i++)
114        {
```
```