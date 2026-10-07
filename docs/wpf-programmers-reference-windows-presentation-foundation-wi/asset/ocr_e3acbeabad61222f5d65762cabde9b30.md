# THEME RESTRICTIONS

I have had bad luck getting Expression Blend to use specific themes. It seems to have trouble finding the DLLs for use by the ResourceDictionary's Source property. I've also had bad luck getting the compiled executable to run.

Perhaps these issues will be fixed in a later release, but for now I use this technique to see what the program will look like in different themes in programs with Visual Studio. If you figure out how to get these working in Expression Blend, e-mail me at RodStephens@vb-helper.com and I'll post your solutions on the book's web page.

# SKINS

Themes let a program automatically change to match the rest of the system's appearance. Selecting a specific theme lets a program change its appearance deliberately, but that's generally not necessary. The differences between Luna Metallic and Aero Normal themes are so small that there's little reason to force the user to use one or the other when you could let the program use the system's default theme.

Skins are much more interesting. A skin is a packaged set of appearances and behaviors that can give an application (or part of an application) a distinctive appearance while still allowing it to provide its key features.

Skins are somewhat similar to themes in the sense that they define the appearance and behavior of an application, but they generally make larger changes in the application's appearance than those shown in Figures 16-1 and 16-3. Rather unifying all of the applications running on a system, the larger changes provided by skins can make an application stand out. A skin differentiates the application and makes it easier for the user to tell applications apart at a glance.

For example, Figures 16-5 and 16-6 show the ResourceDictionaries example program (which is described in Chapter 12) displaying two different appearances. It's the same program in both figures and it contains the same controls—just rearranged slightly with different colors, fonts, and so forth.

![](bbox=[0.125, 0.718, 0.625, 0.853])

FIGURE 16-5