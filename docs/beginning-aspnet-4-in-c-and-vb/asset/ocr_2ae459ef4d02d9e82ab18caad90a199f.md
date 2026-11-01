The following table lists the changes for the French version.

| FRENCH NAME | VALUE |
|---|---|
| $this.Text (title of the form) | Le livre du jour |
| labelItemsSold.Text | Des livres vendus: |
| labelBookOfTheDay.Text | Le livre du jour: |

By default, images are not moved to satellite assemblies. However, in the sample application, the flag should be different depending on the country. To achieve this, you have to add the image of the American flag to the file Resources.resx. You can find this file in the Properties section of the Visual Studio Solution Explorer. With the resource editor, select the Images category, as shown in Figure 22-9, and add the file americanflag.bmp. To make localization with images possible, the image must have the same name in all languages. Here, the image in the file Resources.resx has the name Flag. You can rename the image in the properties editor.

![](bbox=[0.52, 0.33, 0.88, 0.55])

FIGURE 22-9

Within the properties editor, you can also change whether the image should be linked or embedded. For best performance with resources, images are linked by default. With linked images, the image file must be delivered together with the application. If you want to embed the image within the assembly, you can change the Persistence property to Embedded.

The localized versions of the flags can be added by copying the file Resource.resx to Resource.de.resx and Resource.fr.resx and replacing the flags with GermanFlag.bmp and FranceFlag.bmp. Because a strongly typed resource class is needed only with the neutral resource, the property CustomTool can be cleared with the resource files of all specific languages.

Compiling the project now creates a satellite assembly for each language. Inside the debug directory (or the release, depending on your active configuration), language subdirectories like de and fr are created. In such a subdirectory, you will find the file BookOfTheDay.resources.dll. Such a file is a satellite assembly that includes only localized resources. Opening this assembly with ildasm, you see a manifest with the embedded resources and a defined locale. The assembly has the locale de in the assembly attributes, so it can be found in the de subdirectory. You can also see the name of the resource with .resource; it is prefixed with the namespace name Wrox.ProCSharp.Localization, followed by the class name BookOfTheDayForm and the language code de.

# Changing the Culture Programmatically

After translating the resources and building the satellite assemblies, you will get the correct translations according to the configured culture for the user. The welcome message is not translated at this time. This needs to be done in a different way, as you'll see shortly.

In addition to the system configuration, it should be possible to send the language code as a command-line argument to your application for testing purposes. The BookOfTheDayForm constructor is changed to allow the passing of a culture string and the setting of the culture according to this string. A CultureInfo instance is created to pass it to the CurrentCulture and CurrentUICulture properties of the current thread. Remember that the CurrentCulture is used for formatting, and the CurrentUICulture is used for loading resources.