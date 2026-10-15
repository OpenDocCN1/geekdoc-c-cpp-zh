# LISTING 8.22 continued

```
//------------------------------------------------------------
// Draws the image in the current location.
//------------------------------------------------------------
public void paintComponent (Graphics page)
{
    super.paintComponent (page);
    currentImage.paintIcon (this, page, x, y);
}

//****************************************************************
// Represents the listener for keyboard activity.
//****************************************************************
private class DirectionListener implements KeyListener
{
    //------------------------------------------------------------
    // Responds to the user pressing arrow keys by adjusting the
    // image and image location accordingly.
    //------------------------------------------------------------
    public void keyPressed (KeyEvent event)
    {
        switch (event.getKeyCode())
        {
            case KeyEvent.VK_UP:
                currentImage = up;
                y -= JUMP;
                break;
            case KeyEvent.VK_DOWN:
                currentImage = down;
                y += JUMP;
                break;
            case KeyEvent.VK_LEFT:
                currentImage = left;
                x -= JUMP;
                break;
            case KeyEvent.VK_RIGHT:
                currentImage = right;
                x += JUMP;
                break;
        }

        repaint();
    }
}
```