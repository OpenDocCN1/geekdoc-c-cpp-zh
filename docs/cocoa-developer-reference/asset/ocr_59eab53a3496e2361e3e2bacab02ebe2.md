# Figure 15.9

Assigning a standard system file type to the document

![](bbox=[0.158, 0.191, 0.704, 0.501])

Adding a custom UTI is a labor-intensive process. You must define it in your application’s info.plist file, which is an XML document with a variety of application settings. Xcode includes a plist editor, but it’s easier to navigate to your project’s folder in Finder, open the plist file in a text editor, copy the UTI boilerplate XML from Apple’s documentation, paste it into the plist file, and make minor edits by hand. Sample XML to create a custom UTI that implements an abcd file extension follows:

```
    <key>UTExportedTypeDeclarations</key>
        <array>
            <dict>
                <key>UTTypeIdentifier</key>
                <string>com.myURL.applicationname</string>
                <key>UTTypeDescription</key>
                <string>My custom document format</string>
                <key>UTTypeConformsTo</key>
                <array>
                    <string>public.data</string>
                </array>
                <key>UTTypeTagSpecification</key>
                <dict>
                    <key>com.apple.ostype</key>
                    <string>abcd</string>
```