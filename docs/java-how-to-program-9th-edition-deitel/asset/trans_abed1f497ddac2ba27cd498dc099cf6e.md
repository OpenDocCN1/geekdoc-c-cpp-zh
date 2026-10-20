

and are added to menu bars or to other menus as submenus. When a menu is clicked, it expands to show its list of menu items.

类 **JMenuItem**（`javax.swing.AbstractButton` 的子类）包含管理菜单项所需的方法。菜单项是菜单内的 GUI 组件，当被选中时会触发一个动作事件。菜单项可用于启动一个动作，或作为提供更多可供用户选择的菜单项的 **submenu**。子菜单用于在菜单中对相关的菜单项进行分组。

类 **JCheckBoxMenuItem**（`javax.swing.JMenuItem` 的子类）包含管理可打开或关闭的菜单项所需的方法。当选择一个 JCheckBoxMenuItem 时，菜单项左侧会出现一个复选标记。当再次选择该 JCheckBoxMenuItem 时，复选标记会被移除。

类 **JRadioButtonMenuItem**（`javax.swing.JMenuItem` 的子类）包含管理像 JCheckBoxMenuItems 一样可打开或关闭的菜单项所需的方法。当多个 JRadioButtonMenuItems 作为 ButtonGroup 的一部分维护时，同一时间组中只有一个项可以被选中。当选择一个 JRadioButtonMenuItem 时，菜单项左侧会出现一个填充的圆圈。当选择另一个 JRadioButtonMenuItem 时，先前选中菜单项的填充圆圈会被移除。

## Using Menus in an Application

Figures 25.5–25.6 demonstrate various menu items and how to specify special characters called mnemonics that can provide quick access to a menu or menu item from the keyboard. Mnemonics can be used with all subclasses of `javax.swing.AbstractButton`. Class MenuFrame (Fig. 25.5) creates the GUI and handles the menu-item events. Most of the code in this application appears in the class’s constructor (lines 34–151).

```java
// Fig. 25.5: MenuFrame.java
// Demonstrating menus.
import java.awt.Color;
import java.awt.Font;
import java.awt.BorderLayout;
import java.awt.event.ActionListener;
import java.awt.event.ActionEvent;
import java.awt.event.ItemListener;
import java.awt.event.ItemEvent;
import javax.swing.JFrame;
import javax.swing.JRadioButtonMenuItem;
import javax.swing.JCheckBoxMenuItem;
import javax.swing.JOptionPane;
import javax.swing.JLabel;
import javax.swing.SwingConstants;
import javax.swing.ButtonGroup;
import javax.swing.JMenu;
import javax.swing.JMenuItem;
import javax.swing.JMenuBar;

public class MenuFrame extends JFrame
{
```

```
76  bar.add( fileMenu ); // add file menu to menu bar
77

78  JMenu formatMenu = new JMenu( "Format" ); // create format menu
79  formatMenu.setMnemonic( 'r' ); // set mnemonic to r
80

81  // array listing string colors
82  String[] colors = { "Black", "Blue", "Red", "Green" };
83

84  JMenu colorMenu = new JMenu( "Color" ); // create color menu
85  colorMenu.setMnemonic( 'C' ); // set mnemonic to C
86

87  // create radio button menu items for colors
88  colorItems = new JRadioButtonMenuItem[ colors.length ];
89  colorButtonGroup = new ButtonGroup(); // manages colors
90  ItemHandler itemHandler = new ItemHandler(); // handler for colors
91

92  // create color radio button menu items
93  for ( int count = 0; count < colors.length; count++ )
94  {
95      colorItems[ count ] =
96      new JRadioButtonMenuItem( colors[ count ] ); // create item
97      colorMenu.add( colorItems[ count ] ); // add item to color menu
98      colorButtonGroup.add( colorItems[ count ] ); // add to group
99      colorItems[ count ].addActionListener( itemHandler );
100 } // end for
101

102 colorItems[ 0 ].setSelected( true ); // select first Color item
103

104 formatMenu.add( colorMenu ); // add color menu to format menu
105 formatMenu.addSeparator(); // add separator in menu
106

107 // array listing font names
108 String[] fontNames = { "Serif", "Monospaced", "SansSerif" };
109 JMenu fontMenu = new JMenu( "Font" ); // create font menu
110 fontMenu.setMnemonic( 'n' ); // set mnemonic to n
111

112 // create radio button menu items for font names
113 fonts = new JRadioButtonMenuItem[ fontNames.length ];
114 fontButtonGroup = new ButtonGroup(); // manages font names
115

116 // create Font radio button menu items
117 for ( int count = 0; count < fonts.length; count++ )
118 {
119     fonts[ count ] = new JRadioButtonMenuItem( fontNames[ count ] );
120     fontMenu.add( fonts[ count ] ); // add font to font menu
121     fontButtonGroup.add( fonts[ count ] ); // add to button group
122     fonts[ count ].addActionListener( itemHandler ); // add handler
123 } // end for
124

125 fonts[ 0 ].setSelected( true ); // select first Font menu item
126 fontMenu.addSeparator(); // add separator bar to font menu
127

128 String[] styleNames = { "Bold", "Italic" }; // names of styles
```

```
129  styleItems = new JCheckBoxMenuItem[ styleNames.length ];
130  StyleHandler styleHandler = new StyleHandler(); // style handler
131

132  // create style checkbox menu items
133  for ( int count = 0; count < styleNames.length; count++ )
134  {
135      styleItems[ count ] =
136          new JCheckBoxMenuItem( styleNames[ count ] ); // for style
137      fontMenu.add( styleItems[ count ] ); // add to font menu
138      styleItems[ count ].addItemListener( styleHandler ); // handler
139  } // end for
140

141  formatMenu.add( fontMenu ); // add Font menu to Format menu
142  bar.add( formatMenu ); // add Format menu to menu bar
143

144  // set up label to display text
145  displayJLabel = new JLabel( "Sample Text", SwingConstants.CENTER );
146  displayJLabel.setForeground( colorValues[ 0 ] );
147  displayJLabel.setFont( new Font( "Serif", Font.PLAIN, 72 ) );
148

149  getContentPane().setBackground( Color.CYAN ); // set background
150  add( displayJLabel, BorderLayout.CENTER ); // add displayJLabel
151  } // end MenuFrame constructor
152

153  // inner class to handle action events from menu items
154  private class ItemHandler implements ActionListener
155  {
156      // process color and font selections
157      public void actionPerformed( ActionEvent event )
158      {
159          // process color selection
160          for ( int count = 0; count < colorItems.length; count++ )
161          {
162              if ( colorItems[ count ].isSelected() )
163              {
164                  displayJLabel.setForeground( colorValues[ count ] );
165                  break;
166              } // end if
167          } // end for
168

169          // process font selection
170          for ( int count = 0; count < fonts.length; count++ )
171          {
172              if ( event.getSource() == fonts[ count ] )
173              {
174                  displayJLabel.setFont(
175                      new Font( fonts[ count ].getText(), style, 72 ) );
176              } // end if
177          } // end for
178

179          repaint(); // redraw application
180      } // end method actionPerformed
181  } // end class ItemHandler
```

```
// inner class to handle item events from checkbox menu items
private class StyleHandler implements ItemListener
{
    // process font style selections
    public void itemStateChanged( ItemEvent e )
    {
        String name = displayJLabel.getFont().getName(); // current Font
        Font font; // new font based on user selections

        // determine which items are checked and create Font
        if ( styleItems[ 0 ].isSelected() &&
            styleItems[ 1 ].isSelected() )
            font = new Font( name, Font.BOLD + Font.ITALIC, 72 );
        else if ( styleItems[ 0 ].isSelected() )
            font = new Font( name, Font.BOLD, 72 );
        else if ( styleItems[ 1 ].isSelected() )
            font = new Font( name, Font.ITALIC, 72 );
        else
            font = new Font( name, Font.PLAIN, 72 );

        displayJLabel.setFont( font );
        repaint(); // redraw application
    } // end method itemStateChanged
} // end class StyleHandler
} // end class MenuFrame
```

Fig. 25.5 | JMenus and mnemonics. (Part 5 of 5.)

```
// Fig. 25.6: MenuTest.java
// Testing MenuFrame.
import javax.swing.JFrame;

public class MenuTest
{
    public static void main( String[] args )
    {
        MenuFrame menuFrame = new MenuFrame(); // create MenuFrame
        menuFrame.setDefaultCloseOperation( JFrame.EXIT_ON_CLOSE );
        menuFrame.setSize( 500, 200 ); // set frame size
        menuFrame.setVisible( true ); // display frame
    } // end main
} // end class MenuTest
```

![](img/009e962758dcc71dbc43a493362e6dc0_1048_0.png)

Fig. 25.6 | Test class for MenuFrame. (Part 1 of 2.)

