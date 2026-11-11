

```java
private CompositeComponent canvas;
private JComboBox<Rule> ruleCombo;
private JSlider alphaSlider;
private JTextField explanation;

public CompositeTestFrame()
{
   setSize(DEFAULT_WIDTH, DEFAULT_HEIGHT);

   canvas = new CompositeComponent();
   add(canvas, BorderLayout.CENTER);

   ruleCombo = new JComboBox<>(new Rule[] { new Rule("CLEAR", "  ", "  "),
         new Rule("SRC", " S", " S"), new Rule("DST", "  ", "DD"),
         new Rule("SRC_OVER", " S", "DS"), new Rule("DST_OVER", " S", "DD"),
         new Rule("SRC_IN", "  ", " S"), new Rule("SRC_OUT", " S", "  "),
         new Rule("DST_IN", "  ", " D"), new Rule("DST_OUT", "  ", "D "),
         new Rule("SRC_ATOP", "  ", "DS"), new Rule("DST_ATOP", " S", " D"),
         new Rule("XOR", " S", " D"), });
   ruleCombo.addActionListener(event ->
         {
            Rule r = (Rule) ruleCombo.getSelectedItem();
            canvas.setRule(r.getValue());
            explanation.setText(r.getExplanation());
         });

   alphaSlider = new JSlider(0, 100, 75);
   alphaSlider.addChangeListener(event -> canvas.setAlpha(alphaSlider.getValue()));
   JPanel panel = new JPanel();
   panel.add(ruleCombo);
   panel.add(new JLabel("Alpha"));
   panel.add(alphaSlider);
   add(panel, BorderLayout.NORTH);

   explanation = new JTextField();
   add(explanation, BorderLayout.SOUTH);

   canvas.setAlpha(alphaSlider.getValue());
   Rule r = ruleCombo.getItemAt(ruleCombo.getSelectedIndex());
   canvas.setRule(r.getValue());
   explanation.setText(r.getExplanation());
}
```

## AFL-CIO 领袖

有些人天生就是领导者。有些人在平静的绝望中度过一生，无法挣脱束缚他们的枷锁。有些人则因其性格和境遇的本质而被召唤去领导。约翰·多伊就是这样一个人，他的一生见证了信念的力量和人类精神的力量。

约翰·多伊出生于俄亥俄州一个小镇上一个收入微薄的家庭，很小就懂得了辛勤工作的价值。他的父亲是一名煤矿工人，在矿井里长时间辛苦劳作；他的母亲是一名学校教师，培养了他对学习的热爱和深厚的正义感。这些早年的教诲塑造了他后来成为的人。

完成学业后，约翰·多伊开始在铁路部门工作，在那里他亲眼目睹了劳动男女的挣扎。正是在这里，他参与了劳工运动，加入了铁路职员兄弟会。他的奉献精神和领导才能迅速推动他担任越来越重要的职位。

在整个职业生涯中，约翰·多伊捍卫工人权利，争取公平工资、更好的工作条件和工作保障。他不懈的努力并非没有牺牲；他面临反对、挫折甚至威胁，但他从未动摇对劳工事业的承诺。

最终，他的领导才能和远见使他走上 AFL-CIO 的前沿，在那里他担任重要领导人，为工人阶级发声，并塑造了惠及数百万人的政策。约翰·多伊的遗产不仅在于他担任过的职位，更在于他触及的生命以及他为无数工人恢复的尊严。

```java
    /**
     * Sets the alpha of the source.
     * @param a the alpha value between 0 and 100
     */
    public void setAlpha(int a)
    {
        alpha = (float) a / 100.0F;
        repaint();
    }
    }
```

### 清单 11.5 composite/Rule.java

```java
    package composite;

    import java.awt.*;

    /**
     * This class describes a Porter-Duff rule.
     */
    class Rule
    {
        private String name;
        private String porterDuff1;
        private String porterDuff2;

        /**
         * Constructs a Porter-Duff rule.
         * @param n the rule name
         * @param pd1 the first row of the Porter-Duff square
         * @param pd2 the second row of the Porter-Duff square
         */
        public Rule(String n, String pd1, String pd2)
        {
            name = n;
            porterDuff1 = pd1;
            porterDuff2 = pd2;
        }

        /**
         * Gets an explanation of the behavior of this rule.
         * @return the explanation
         */
        public String getExplanation()
        {
```

### 清单 11.5（续）

```java
33  StringBuilder r = new StringBuilder("Source ");
34  if (porterDuff2.equals(" ")) r.append("clears");
35  if (porterDuff2.equals("S")) r.append("overwrites");
36  if (porterDuff2.equals("DS")) r.append("blends with");
37  if (porterDuff2.equals("D")) r.append("alpha modifies");
38  if (porterDuff2.equals("D")) r.append("alpha complement modifies");
39  if (porterDuff2.equals("DD")) r.append("does not affect");
40  r.append(" destination");
41  if (porterDuff2.equals(" S")) r.append(" and overwrites empty pixels");
42  r.append(".");
43  return r.toString();
44 }
45
46 public String toString()
47 {
48    return name;
49 }
50
51 /**
52  * Gets the value of this rule in the AlphaComposite class.
53  * @return the AlphaComposite constant value, or -1 if there is no matching constant
54  */
55 public int getValue()
56 {
57    try
58    {
59       return (Integer) AlphaComposite.class.getField(name).get(null);
60    }
61    catch (Exception e)
62    {
63       return -1;
64    }
65 }
66 }
```

### java.awt.Graphics2D 1.2

- `void setComposite(Composite s)`  
  将此图形上下文的合成设置为实现 Composite 接口的给定对象。

### java.awt.AlphaComposite 1.2

- `static AlphaComposite getInstance(int rule)`
- `static AlphaComposite getInstance(int rule, float sourceAlpha)`

构造一个 alpha 合成对象。规则是 CLEAR、SRC、SRC_OVER、DST_OVER、SRC_IN、SRC_OUT、DST_IN、DST_OUT、DST_ATOP、SRC_ATOP、XOR 之一。

## 11.9 渲染提示

在前面的章节中，你已经看到渲染过程相当复杂。尽管 Java 2D API 在大多数情况下快得惊人，但有时你希望控制速度与质量之间的权衡。你可以通过设置*渲染提示*来实现这一点。`Graphics2D` 类的 `setRenderingHint` 方法允许你设置单个提示。这些提示的键和值在 `RenderingHints` 类中声明。表 11.2 总结了这些选项。以 `_DEFAULT` 结尾的值表示特定实现所选择的默认值，作为性能与质量之间的良好权衡。

### 表 11.2 渲染提示

| 键 | 值 | 说明 |
| --- | --- | --- |
| KEY_ANTIALIASING | VALUE_ANTIALIAS_ON<br>VALUE_ANTIALIAS_OFF<br>VALUE_ANTIALIAS_DEFAULT | 打开或关闭形状的抗锯齿。 |
| KEY_TEXT_ANTIALIASING | VALUE_TEXT_ANTIALIAS_ON<br>VALUE_TEXT_ANTIALIAS_OFF<br>VALUE_TEXT_ANTIALIAS_DEFAULT<br>VALUE_TEXT_ANTIALIAS_GASP ⑥<br>VALUE_TEXT_ANTIALIAS_LCD_HRGB ⑥<br>VALUE_TEXT_ANTIALIAS_LCD_HBGR ⑥<br>VALUE_TEXT_ANTIALIAS_LCD_VRGB ⑥<br>VALUE_TEXT_ANTIALIAS_LCD_VBGR ⑥ | 打开或关闭字体的抗锯齿。使用 VALUE_TEXT_ANTIALIAS_GASP 值时，会查询字体的“gasp 表”来决定特定字号的字体是否应进行抗锯齿。LCD 值会强制对特定显示类型进行子像素渲染。 |
| KEY_FRACTIONALMETRICS | VALUE_FRACTIONALMETRICS_ON<br>VALUE_FRACTIONALMETRICS_OFF<br>VALUE_FRACTIONALMETRICS_DEFAULT | 打开或关闭分数字符尺寸的计算。分数字符尺寸可以改善字符的放置。 |
| KEY_RENDERING | VALUE_RENDER_QUALITY<br>VALUE_RENDER_SPEED<br>VALUE_RENDER_DEFAULT | 在可用时，选择渲染算法以获得更高质量或更快速度。 |
| KEY_STROKE_CONTROL 1.3 | VALUE_STROKE_NORMALIZE<br>VALUE_STROKE_PURE<br>VALUE_STROKE_DEFAULT | 选择描边的位置由图形加速器控制（可能将其移动最多半个像素），还是由“纯”规则计算，该规则要求描边穿过像素中心。 |
| KEY_DITHERING | VALUE_DITHER_ENABLE<br>VALUE_DITHER_DISABLE<br>VALUE_DITHER_DEFAULT | 打开或关闭颜色抖动。抖动通过绘制颜色相近的像素组来近似颜色值。（注意，抗锯齿可能会干扰抖动。） |
| KEY_ALPHA_INTERPOLATION | VALUE_ALPHA_INTERPOLATION_QUALITY<br>VALUE_ALPHA_INTERPOLATION_SPEED<br>VALUE_ALPHA_INTERPOLATION_DEFAULT | 打开或关闭 alpha 合成的精确计算。 |
| KEY_COLOR_RENDERING | VALUE_COLOR_RENDER_QUALITY<br>VALUE_COLOR_RENDER_SPEED<br>VALUE_COLOR_RENDER_DEFAULT | 选择颜色渲染的质量或速度。仅当使用不同的颜色空间时，这才成为问题。 |
| KEY_INTERPOLATION | VALUE_INTERPOLATION_NEAREST_NEIGHBOR<br>VALUE_INTERPOLATION_BILINEAR<br>VALUE_INTERPOLATION_BICUBIC | 选择缩放或旋转图像时插值像素的规则。 |

这些设置中最有用的是抗锯齿。这种技术消除了斜线和曲线上的“锯齿”。如图 11.25 所示，斜线必须被绘制成像素的“阶梯”。特别是在低分辨率屏幕上，这条线可能看起来很难看。但是，如果不是将每个像素完全绘制为开或关，而是用与该线覆盖像素面积成比例的颜色值给部分覆盖的像素着色，那么结果看起来会平滑得多。这种技术称为抗锯齿。当然，抗锯齿会稍微耗时一些，因为它必须计算所有这些颜色值。

