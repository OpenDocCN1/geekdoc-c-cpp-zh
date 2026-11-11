```
public void cascadeWindows()
{
   int x = 0;
   int y = 0;
   int width = desktop.getWidth() / 2;
   int height = desktop.getHeight() / 2;

   for (JInternalFrame frame : desktop.getAllFrames())
   {
      if (!frame.isIcon())
      {
         try
         {
            // try to make maximized frames resizable; this might be vetoed
            frame.setMaximum(false);
            frame.reshape(x, y, width, height);

            x += frameDistance;
            y += frameDistance;
            // wrap around the desktop edge
            if (x + width > desktop.getWidth()) x = 0;
            if (y + height > desktop.getHeight()) y = 0;
         }
         catch (PropertyVetoException ex)
         {
         }
      }
   }
}

/**
 * Tiles the noniconified internal frames of the desktop.
 */
public void tileWindows()
{
   // count frames that aren't iconized
   int frameCount = 0;
   for (JInternalFrame frame : desktop.getAllFrames())
      if (!frame.isIcon()) frameCount++;
   if (frameCount == 0) return;

   int rows = (int) Math.sqrt(frameCount);
   int cols = frameCount / rows;
   int extra = frameCount % rows;
   // number of columns with an extra row

   int width = desktop.getWidth() / cols;
   int height = desktop.getHeight() / rows;
   int r = 0;
```

(Continues)