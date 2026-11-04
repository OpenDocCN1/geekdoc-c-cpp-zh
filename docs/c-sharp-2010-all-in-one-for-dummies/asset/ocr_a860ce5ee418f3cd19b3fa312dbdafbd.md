which is how the snippet is referred. The Snippet element, where all the work is done, includes a Code element, which has the code to be inserted.

The best way to make a new snippet is to modify an existing one. Snippets can be found in your Visual Studio install directory, which should be C:\Program Files (x86)\Microsoft Visual Studio 10.0\VC\# Snippets\1033 if you are on a 64-bit operating system (otherwise you can drop the x86).

In the folder referenced in the preceding paragraph, let's look at a simple example: cw. snippet is a Console.WriteLine command. Right-click the file to open it. Here's the code:

```
```xml
<?xml version="1.0" encoding="utf-8" ?>
<CodeSnippets xmlns="http://schemas.microsoft.com/VisualStudio/2005/CodeSnippet">
  <CodeSnippet Format="1.0.0">
    <Header>
      <Title>cw</Title>
      <Shortcut>cw</Shortcut>
      <Description>Code snippet for Console.WriteLine</Description>
      <Author>Microsoft Corporation</Author>
      <SnippetTypes>
        <SnippetType>Expansion</SnippetType>
      </SnippetTypes>
    </Header>
    <Snippet>
      <Declarations>
        <Literal Editable="false">
          <ID>System.Console</ID>
          <Function>SimpleTypeName(global::System.Console)</Function>
        </Literal>
      </Declarations>
      <Code Language="csharp">
        <![CDATA[$SystemConsole$.WriteLine($end$);]]>
      </Code>
    </Snippet>
  </CodeSnippet>
</CodeSnippets>
```
```

This list describes what's in the Header element:

+   - **Title:** Shows up on the context menu.
+   - **Shortcut:** The key combination you can type for IntelliSense.
+   - **Description and Author:** Show up in the tooltip when you mouse over the snippet in Visual Studio.
+   - **SnippetType:** Defines which menus the snippet appears on. The most common types are Expansion and SurroundsWith. *Expansion* means that it inserts the text. *SurroundsWith* means that it's placed above and below the selection.