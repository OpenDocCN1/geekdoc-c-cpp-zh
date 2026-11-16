```
} catch (IOException ioex) {
    ioex.printStackTrace();
} finally {
    try {
        out.close();
        System.out.println("Wrote: " + file.getPath());
    } catch (Exception ex) { }
}
```

```
public void writeOutStrings(String fileName) {
    System.out.println();
    System.out.println();
    System.out.printIn("***************************");
    // We read with a BufferedReader, and write with
    // Expect a BufferedWriter, but no...
    // Damn Java, a PrintWriter.
    // Is there a PrintReader? No. Why? No idea.
    String[] strings = {
        "Lorem ipsum dolor sit amet, consectetuer adipiscing elit.",
        "sed do eiusmod tempor incididunt ut labore et dolore magna",
        "aliqua. Ut enim ad minim veniam, quis nostrud exercitation",
        "ullamco laboris nisi ut aliquip ex ea commodo consequat.",
        "Duis aute irure dolor in reprehenderit in voluptate velit",
        "esse cillum dolore eu fugiat nulla pariatur. Excepteur sint",
        "occaecat cupidatat non proident, sunt in culpa qui officia",
        "deserunt mollit anim id est laborum.",
    };
```

```
File file = new File(fileName);
PrintWriter out = null;
try {
    out = new PrintWriter(file);
    for (String string : strings) {
        out.println(string);
    }
} catch (FileNotFoundException fex) {
    fex.printStackTrace();
} finally {
    try {
        out.close();
        System.out.println("Wrote: " + file.getPath());
```