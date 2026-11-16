

```java
// draw Descent
g2d.setColor( Color.RED );
propY = y + (int)tl.getDescent();
g2d.drawLine( xLeft, propY, xRight, propY );
g2d.drawString( "Descent", xRight, propY );

// draw Leading
g2d.setColor( Color.GREEN );
propY = y + (int)tl.getDescent() + (int)tl.getLeading();
g2d.drawLine( xLeft, propY, xRight, propY );
temp = new TextLayout(
    "Descent", propFont, g2d.getFontRenderContext() );
g2d.drawString( "Leading", xRight + temp.getVisibleAdvance(), propY );

// draw console output...
g2d.setColor( Color.LIGHT_GRAY );
g2d.setFont( new Font( "Courier New", Font.BOLD, 12 ) );
Utility.drawString( g2d, 20, 300, console );

}

private String toString( Rectangle2D r ) {
    return "[ x=" + r.getX() + ", y=" + r.getY() + ", w=" + r.getWidth()
        + ", h=" + r.getHeight() + "]";
}

public static void main( String[] args ) {
    launchApp( new TextMetricsExample() );
}
}
```

![](img/588a4cda8f2acae94a7e1987bf99400d_349_0.png)

图 11.6 文本布局示例。© 2014 Timothy Wright。

TextLayoutExample 如图 11.6 所示，位于 javagames.text 包中，它使用字体信息绘制复古风格的高分输入屏幕。initialize() 方法负责计算每个字母的宽度以确定最大宽度。由于 graphics 对象在 initialize() 方法中尚不可用，因此会出现一个问题。处理此问题有两种方法。一种方法是从 JFrame 类获取字体度量对象：

```
Font font = new Font(...);
FontMetrics fm = this.getFontMetrics(font);
```

第二种方法是让 JFrame 通过提供一个 Font 对象来创建 FontMetrics 对象。然而，这两种解决方案都需要访问 JFrame 对象。如果当前类无法访问 JFrame，那么获取字体计算所需的 FontMetrics 对象的另一种方法是创建一个图像并使用其 Graphics 对象。

```
BufferedImage img = new BufferedImage(1, 1, BufferedImage.TYPE_INT_ARGB);
Graphics2D g = img.createGraphics();
FontMetrics fm = g.getFontMetrics(font);
g.dispose();
```

虽然从头创建新图像需要一些代码，但如果无法使用 JFrame 类，这是一个可选方案。

```
package javagames.text;
```

```
import java.awt.*;
import java.awt.RenderingHints;
import java.awt.image.BufferedImage;
import javagames.util.SimpleFramework;
```

```
public class TextLayoutExample extends SimpleFramework {
 private Font font;
 private int maxWidth;
 public TextLayoutExample() {
 appWidth = 640;
 appHeight = 640;
 appSleep = 10L;
 appTitle = "Text Layout Example";
 appBackground = Color.WHITE;
 appFPSColor = Color.BLACK;
 }
```

```
@Override
protected void initialize() {
    super.initialize();
    font = new Font( "Arial", Font.BOLD, 40 );
    FontMetrics fm = getFontMetrics( font );
    maxWidth = Integer.MIN_VALUE;
    for( int i = (int)'!'; i < (int)'z'; ++i ) {
        String letter = "" + (char)i;
        maxWidth = Math.max( maxWidth, fm.stringWidth( letter ) );
    }
}
// another way
BufferedImage img =
new BufferedImage( 1, 1, BufferedImage.TYPE_INT_ARGB );
Graphics2D g = img.createGraphics();
FontMetrics fontMetrics = g.getFontMetrics( font );
g.dispose();
}
```

```
@Override
protected void render( Graphics g ) {
    super.render( g );
    Graphics2D g2d = (Graphics2D)g;
    g2d.setRenderingHint( RenderingHints.KEY_ANTIALIASING,
    RenderingHints.VALUE_ANTIALIAS_ON );
    g2d.setColor( Color.GREEN );
    g2d.setFont( font );
    FontMetrics fm = g2d.getFontMetrics();
    int height = fm.getAscent() + fm.getDescent() + fm.getLeading();
    int x = 20;
    int y = 50;
    y += fm.getAscent();
    int count = 0;
    for( int i = (int)'!'; i < (int)'z'; ++i ) {
        String letter = "" + (char)i;
        g2d.drawString( letter, x, y );
        x += maxWidth;
        count++;
        if( count % 10 == 0 ) {
            y += height;
            x = 20;
        }
    }
}
```

```
public static void main(String[] args) {
   launchApp( new TextLayoutExample() );
}
}
```

![](img/588a4cda8f2acae94a7e1987bf99400d_352_0.png)

图 11.7 控制台覆盖层示例。© 2014 Timothy Wright。

ConsoleOverlayExample 如图 11.7 所示，位于 `javagames.text` 包中，它结合文本位置和透明度来创建一个可滚动并自动隐藏的文本控制台。`initialize()` 方法创建 Font 并计算字体高度。滚动文本在 Vector 对象中创建。第一行文本被复制到底部以实现滚动。控制台被设置为文本高度加上一行额外的高度，但由于顶行被复制，实际上有两行额外的高度。

`processInput()` 方法负责两件事。首先，它监视鼠标，并在鼠标位于控制台范围内时更新透明度。其次，每当按下空格键时，它就会启动滚动文本，使用 B 键切换滚动文本框，并使用 H 键显示或隐藏控制台。

`updateObjects()` 方法负责处理控制台状态。首先用灰色背景填充控制台，然后将文本绘制到背景上。随后在文本上绘制滚动框，或者绘制绿色矩形以显示框的位置。

hidden 值变量是一个从零到一的浮点数，其中一表示完全隐藏，零表示完全可见。根据控制台是显示还是隐藏，hidden 值会使用 delta 时间值进行更新，以缓慢显示或隐藏控制台。如果 hidden 值尚未为零，则使用 AlphaComposite 对象清除控制台每一侧的一部分。这使得控制台可以在任何背景上变得可见。

### 注意

AlphaComposite 类和透明度在第 10 章“图像”中介绍。如果 ConsoleOverlayExample 中的任何代码不清楚，请复习该章节。

render() 方法创建棋盘格背景，设置 AlphaComposite，并将文本控制台叠加到背景图像上。

```
package javagames.text;
import java.awt.*;
import java.awt.event.KeyEvent;
import java.awt.image.BufferedImage;
import java.util.Vector;
import javagames.util.*;
public class ConsoleOverlayExample extends SimpleFramework {
	private BufferedImage console;
	private int xConsole;
	private int yConsole;
	private float alpha;
	private Font consoleFont;
	private int fontHeight;
	private Vector<String> text;
	private float currY;
	private boolean boxes;
	private boolean hide;
	private float hidden;
	public ConsoleOverlayExample() {
		appWidth = 640;
		appHeight = 640;
		appSleep = 10L;
		appTitle = "Console Overlay Example";
	}
	@Override
	protected void initialize() {
		super.initialize();
		consoleFont = new Font( "Courier New", Font.BOLD, 20 );
		FontMetrics fm = getFontMetrics( consoleFont );
		fontHeight = fm.getAscent() + fm.getDescent() + fm.getLeading();
		currY = 0;
		text = new Vector<String>();
		text.add( "Press the 'H' key to" );
		text.add( "show and hide the console." );
		text.add( "Hover the mouse over the" );
		text.add( "text to change transparency." );
		text.add( "Press Space Bar to move text." );
		text.add( "Press 'B' to toggle hidden boxes." );
		text.add( 0, text.lastElement() );
		int consoleHeight = fontHeight * ( text.size() + 1 );
		console = new BufferedImage(
			canvas.getWidth() - 40,
			consoleHeight,
			BufferedImage.TYPE_INT_ARGB
		);
		xConsole = 20;
		yConsole = 50;
		hide = false;
		hidden = 1.0f;
	}
	@Override
	protected void processInput( float delta ) {
		super.processInput( delta );
		Point pos = mouse.getPosition();
		int minX = xConsole;
		int minY = yConsole;
		int maxX = minX + console.getWidth();
		int maxY = minY + console.getHeight();
		if ( pos.x > minX && pos.x < maxX &&
			pos.y > minY && pos.y < maxY ) {
			alpha = 1.0f;
		} else {
			alpha = 0.75f;
		}
		if ( keyboard.keyDownOnce( KeyEvent.VK_SPACE ) ) {
			text.remove( 0 );
			text.add( text.get( 0 ) );
			currY = fontHeight;
		}
	}
```

