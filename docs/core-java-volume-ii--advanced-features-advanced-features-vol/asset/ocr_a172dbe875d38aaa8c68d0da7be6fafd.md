```
   23
   24  canvas = new CompositeComponent();
   25  add(canvas, BorderLayout.CENTER);
   26
   27  ruleCombo = new JComboBox(new Rule[] { new Rule("CLEAR", "  ", " "),
   28      new Rule("SRC", " S", " S"), new Rule("DST", "  ", " DD"),
   29      new Rule("SRC_OVER", " S", " DS"), new Rule("DST_OVER", " S", " DD"),
   30      new Rule("SRC_IN", "  ", " S"), new Rule("SRC_OUT", " S", "  "),
   31      new Rule("DST_IN", " D", " S"), new Rule("DST_OUT", " D", "  "),
   32      new Rule("SRC_ATOP", "  ", " DS"), new Rule("DST_ATOP", " S", " D"),
   33      new Rule("XOR", " S", " D"), });
   34  ruleCombo.addActionListener(event ->
   35      {
   36          var r = (Rule) ruleCombo.getSelectedItem();
   37          canvas.setRule(r.getValue());
   38          explanation.setText(r.getExplanation());
   39      });
   40
   41  alphaSlider = new JSlider(0, 100, 75);
   42  alphaSlider.addChangeListener(event -> canvas.setAlpha(alphaSlider.getValue()));
   43  var panel = new JPanel();
   44  panel.add(ruleCombo);
   45  panel.add(new JLabel("Alpha"));
   46  panel.add(alphaSlider);
   47  add(panel, BorderLayout.NORTH);
   48
   49  explanation = new JTextField();
   50  add(explanation, BorderLayout.SOUTH);
   51
   52  canvas.setAlpha(alphaSlider.getValue());
   53  Rule r = ruleCombo.getItemAt(ruleCombo.getSelectedIndex());
   54  canvas.setRule(r.getValue());
   55  explanation.setText(r.getExplanation());
   56  }
   57  }
```

# **Listing 11.18** composite/CompositeComponent.java

```
   1  package composite;
   2
   3  import java.awt.*;
   4  import java.awt.geom.*;
   5  import java.awt.image.*;
   6  import javax.swing.*;
   7
   8  /**
   9   * This component draws two shapes, composed with a composition rule.
   10   */
```

*(Continues)*