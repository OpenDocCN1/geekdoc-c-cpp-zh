```
~~~java
46  int n = 10 + generator.nextInt(20);
47  rects.clear();
48  colors.clear();
49  for (int i = 1; i <= n; i++)
50  {
51      int x = generator.nextInt(getWidth());
52      int y = generator.nextInt(getHeight());
53      int width = generator.nextInt(getWidth() - x);
54      int height = generator.nextInt(getHeight() - y);
55      rects.add(new Rectangle(x, y, width, height));
56      int r = generator.nextInt(256);
57      int g = generator.nextInt(256);
58      int b = generator.nextInt(256);
59      colors.add(new Color(r, g, b));
60  }
61  repaint();
62  }
63  
64  public void paintComponent(Graphics g)
65  {
66      if (rects.size() == 0) noDrawing();
67      Graphics2D g2 = (Graphics2D) g;
68  
69      // draw all rectangles
70      for (int i = 0; i < rects.size(); i++)
71      {
72          g2.setPaint(colors.get(i));
73          g2.fill(rects.get(i));
74      }
75  }
76  
77  /**
78   * Creates an SVG document of the current drawing.
79   * @return the DOM tree of the SVG document
80   */
81  public Document buildDocument()
82  {
83      String namespace = "http://www.w3.org/2000/svg";
84      Document doc = builder.newDocument();
85      Element svgElement = doc.createElementNS(namespace, "svg");
86      doc.appendChild(svgElement);
87      svgElement.setAttribute("width", "" + getWidth());
88      svgElement.setAttribute("height", "" + getHeight());
89      for (int i = 0; i < rects.size(); i++)
90      {
~~~
```