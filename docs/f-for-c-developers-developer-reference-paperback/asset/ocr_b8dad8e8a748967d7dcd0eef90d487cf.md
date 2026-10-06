# Some Useful Add-ins

Visual Studio is a powerful editor with a rich set of editing features. However, some Visual Studio add-ins for F# are still recommended as a way to improve your coding experience.

+   - F depth colorizer Because F# uses space senses to indent the code, you can run into seemingly weird errors only because an extra space is needed 10 lines earlier. This extension can highlight this type of indentation problem. This add-in is used to help align code blocks using different colors. I strongly recommend that you install it if your project gets big. You can download it from the Visual Studio gallery at http://visualudiostallallery.msdn.microsoft.com/0713522e-27e6-463f-830a-cb8f0e467c4. Figure 1-11 shows an example of the F# depth colorizer.

```
type blah() =
  let bar()
  member this.Bar()
  let x = 4
  if true then
    bar()
    if true then
      bar()
}
```

FIGURE 1-11 The F# depth colorizer

+   - F# code snippet The code snippet add-in brings the common code—for example, the class definition—to your fingertips. Unlike the C# snippet, the F# snippet also adds any needed dynamic-link library (DLL) references to the project. You can download the add-in and snippet files from http://visualstudiogallery.microsoft.com/d19080ad-d44c-46ae-b65c-55de5f708. An example of the extension in use is shown in Figure 1-12. The configuration options that the tools provide are shown in Figure 1-13.

| | |
|---|---|
| class | Code snippet for class |
| classex |

```
type MyClass() = class
  class name
end
```

FIGURE 1-12 The F# code snippet