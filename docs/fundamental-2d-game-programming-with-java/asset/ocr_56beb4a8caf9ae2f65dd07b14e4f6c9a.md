```
```java
public void loadHighScores() {
    try {
        File file = getHighScoreFile();
        if ( !file.exists() ) {
            createDefaultFile( file );
        }
        parseHighScoreFile( file );
    } catch ( Exception e ) {
        e.printStackTrace();
        handleFileError();
    }
}

private void createDefaultFile( File file ) throws IOException {
    if ( !file.createNewFile() ) {
        throw new IOException();
    }

    String xml = "<hs>\\n";
    for ( String[] score : DEFAULT_SCORES ) {
        xml += "<player name=\"" + score[ 0 ] + "\" score=\"" + score[ 1 ]
            + "\"\\/>\\n";
    }
    xml += "</hs>";

    PrintWriter out = new PrintWriter( new FileWriter( file ) );
    out.write( xml );
    out.flush();
    out.close();
}

private void handleFileError() {
    JOptionPane.showMessageDialog(
        null,
        "Could not create High Score File"
        + "\\nWill not be able to save high scores", "Error",
        JOptionPane.ERROR_MESSAGE
    );

    // Something went wrong, so add scores so the
    // game won't crash...
    for ( String[] score : DEFAULT_SCORES ) {
        scores.add(
            new Score( score[ 0 ], Integer.parseInt( score[ 1 ] ) )
        );
    }
}
```
```