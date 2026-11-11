```
```java
add(label);
logger.exiting("ImageViewerFrame", "<init>");
}

private class FileOpenListener implements ActionListener
{
    public void actionPerformed(ActionEvent event)
    {
        logger.entering("ImageViewerFrame.FileOpenListener", "actionPerformed", event);

        // set up file chooser
        var chooser = new JFileChooser();
        chooser.setCurrentDirectory(new File("."));

        // accept all files ending with .gif
        chooser.setFileFilter(new javax.swing.filechooser.FileFilter()
        {
            public boolean accept(File f)
            {
                return f.getName().toLowerCase().endsWith(".gif") || f.isDirectory();
            }

            public String getDescription()
            {
                return "GIF Images";
            }
        });

        // show file chooser dialog
        int r = chooser.showOpenDialog(ImageViewerFrame.this);

        // if image file accepted, set it as icon of the label
        if (r == JFileChooser.APPROVE_OPTION)
        {
            String name = chooser.getSelectedFile().getPath();
            logger.log(Level.FINE, "Reading file {0}", name);
            label.setIcon(new ImageIcon(name));
        }
        else logger.fine("File open dialog canceled.");
        logger.exiting("ImageViewerFrame.FileOpenListener", "actionPerformed");
    }
}
}

/**
 * A handler for displaying log records in a window.
 */
```
```

_(Continues)_