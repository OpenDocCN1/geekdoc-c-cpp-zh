```
catch( Exception e )
{
    e.printStackTrace();
} // end catch
} // end method init

// DrawJPanel used to display loaded image
private class DrawJPanel extends JPanel
{
    // display image
    public void paintComponent( Graphics g )
    {
        super.paintComponent( g );

        // the following values are used to center the image
        double spareWidth =
            getWidth() - scaleValue * image.getIconWidth();
        double spareHeight =
            getHeight() - scaleValue * image.getIconHeight();

        // draw image with scaled width and height
        g.drawImage( image.getImage(),
            (int)( spareWidth ) / 2, (int)( spareHeight ) / 2,
            (int)( image.getIconWidth() * scaleValue ),
            (int)( image.getIconHeight() * scaleValue ), this );
    } // end method paint
} // end class DrawJPanel
} // end class LoadImageAndScale
```

(a) Java Web Start security dialog that appears because this applet is requesting access to a file on the local computer

![](bbox=[0.26, 0.55, 0.71, 0.74])

(b) Open dialog that appears if the user clicks OK in the security dialog

![](bbox=[0.26, 0.74, 0.79, 0.92])

Fig. 24.1 | Loading, displaying and scaling an image in an applet. (Part 3 of 4.)