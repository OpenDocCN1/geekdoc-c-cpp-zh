# LISTING 7.24

```
p5.setBorder (BorderFactory.createTitledBorder ("Title"));
p5.add (new JLabel ("Titled Border"));
panel.add (p5);

JPanel p6 = new JPanel();
TitledBorder tb = BorderFactory.createTitledBorder ("Title");
tb.setTitleJustification (TitledBorder.RIGHT);
p6.setBorder (tb);
p6.add (new JLabel ("Titled Border (right)"));
panel.add (p6);

JPanel p7 = new JPanel();
Border b1 = BorderFactory.createLineBorder (Color.blue, 2);
Border b2 = BorderFactory.createEtchedBorder ();
p7.setBorder (BorderFactory.createCompoundBorder (b1, b2));
p7.add (new JLabel ("Compound Border"));
panel.add (p7);

JPanel p8 = new JPanel();
Border mb = BorderFactory.createMatteBorder (1, 5, 1, 1,
                                             Color.red);
p8.setBorder (mb);
p8.add (new JLabel ("Matte Border"));
panel.add (p8);

frame.getContentPane().add (panel);
frame.pack();
frame.setVisible(true);
}
}
```

Let’s look at each type of border created in this program. An *empty border* is applied to the larger panel that holds all the others, to create a buffer of space around the outer edge of the frame. The sizes of the top, left, bottom, and right edges of the empty border are specified in pixels. The *line border* is created using a particular color and specifies the line thickness in pixels (3 in this case). The line thickness defaults to 1 pixel if left unspecified. The *etched border* created in this program uses default colors for the highlight and shadow of the etching, but both could be explicitly set if desired.

A *bevel border* can be either raised or lowered. The default coloring is used in this program, although the coloring of each aspect of the bevel can be tailored as