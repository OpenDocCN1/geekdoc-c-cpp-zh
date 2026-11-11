automatically locates the items that are the best match for a given locale. It is easy to add more and more localizations to an existing program—all you have to do is create additional resource bundles.

> > **NOTE:** We simplified the discussion of resource bundle lookup. If a locale has a script or variant, the lookup is quite a bit more complex. See the documentation of the method ResourceBundle.Control.getCandidateLocales for the gory details.

> > **TIP:** You need not place all resources for your application into a single bundle. You could have one bundle for button labels, one for error messages, and so on.

# ### 7.8.2 Property Files

Internationalizing strings is quite straightforward. You place all your strings into a property file such as MyProgramStrings.properties. This is simply a text file with one key/value pair per line. A typical file would look like this:

```
```
computeButton=Rechnen
colorName=Black
defaultPaperSize=210x297
```
```

Then you name your property files as described in the preceding section, for example:

```
```
MyProgramStrings.properties
MyProgramStrings_en.properties
MyProgramStrings_de_DE.properties
```
```

You can load the bundle simply as

```
```
ResourceBundle bundle = ResourceBundle.getBundle("MyProgramStrings", locale);
```
```

To look up a specific string, call

```
```
String computeButtonLabel = bundle.getString("computeButton");
```
```

> > **CAUTION:** Files for storing properties are always ASCII files. If you need to place a Unicode character into a property file, encode it using the \uxxxx encoding. For example, to specify "colorName=Grün", use
> >
> > colorName=Gr\u00FCn
> >
> > You can use the native2ascii tool to generate these files.