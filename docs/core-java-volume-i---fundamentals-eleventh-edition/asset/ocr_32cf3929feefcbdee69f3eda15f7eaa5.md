```
~~~java
49
50    dot.setOnKeyPressed(event ->
51    {
52        KeyCode code = event.getCode();
53        int distance = event.isShiftDown() ? 10 : 1;
54        if (code == KeyCode.DELETE)
55            root.getChildren().remove(dot);
56        else if (code == KeyCode.UP)
57            dot.setCenterY(dot.getCenterY() - distance);
58        else if (code == KeyCode.DOWN)
59            dot.setCenterY(dot.getCenterY() + distance);
60        else if (code == KeyCode.LEFT)
61            dot.setCenterX(dot.getCenterX() - distance);
62        else if (code == KeyCode.RIGHT)
63            dot.setCenterX(dot.getCenterX() + distance);
64    });
65
66    return dot;
67  }
68
69  private void select(Circle dot)
70  {
71      if (selected == dot) return;
72      if (selected != null) selected.setFill(Color.BLACK);
73      selected = dot;
74      if (selected != null)
75      {
76          selected.requestFocus();
77          selected.setFill(Color.RED);
78      }
79  }
80
81  public void start(Stage stage)
82  {
83      root = new Pane();
84      root.setOnMousePressed(event ->
85      {
86          double x = event.getX();
87          double y = event.getY();
88          Circle dot = makeDot(x, y);
89          root.getChildren().add(dot);
90          select(dot);
91      });
92      scene = new Scene(root);
93      root.setPrefSize(PREFERRED_WIDTH, PREFERRED_HEIGHT);
94      stage.setScene(scene);
95      stage.setTitle("MouseTest");
96      stage.show();
97  }
98 }
~~~
```