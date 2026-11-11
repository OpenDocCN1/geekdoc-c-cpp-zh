```
```java
catch (IOException exception)
{
    exception.printStackTrace();
}
});

fileMenu.add(openItem);
exitItem = new JMenuItem("Exit");
exitItem.addActionListener(event -> System.exit(0));
fileMenu.add(exitItem);
pack();
}

/**
 * Prompts the user to select a file, loads the file into a text area, and sets it as the
 * content pane of the frame.
 */
public void openFile() throws IOException
{
    int r = chooser.showOpenDialog(this);
    if (r != JFileChooser.APPROVE_OPTION) return;
    final File f = chooser.getSelectedFile();

    // set up stream and reader filter sequence

    InputStream fileIn = Files.newInputStream(f.toPath());
    final ProgressMonitorInputStream progressIn = new ProgressMonitorInputStream(
        this, "Reading " + f.getName(), fileIn);

    textArea.setText("");

    SwingWorker<Void, Void> worker = new SwingWorker<Void, Void>()
    {
        protected Void doInBackground() throws Exception
        {
            try (Scanner in = new Scanner(progressIn, "UTF-8"))
            {
                while (in.hasNextLine())
                {
                    String line = in.nextLine();
                    textArea.append(line);
                    textArea.append("\n");
                }
            }
            return null;
        }
    };
    worker.execute();
}
}
```
```