Alternatively, scripts can also be attached to empty GameObjects that serve no other function but to hold scripts. So, for instance, an empty GameObject called Script Holder could be created in a scene, and then all the scripts that were in effect in the scene (or most of them anyway) would be attached to that object. This has several benefits; for instance, if someone else picks up the project, they know right where to go to find out what the functionality of the game was. My software developer colleagues always use this sort of mechanism; they are good at reading code and code iterates with each other and find this methodology much, much faster. For the beginner though, this can be tough. The only way to know if an object is being affected by a script is to read through the scripts; trying to discern those tea leaves can be a daunting task. Another important benefit is that method can often keep prefabs intact. When a script is hung off a prefab, it breaks it, or simply makes it so it's not tied to the original any longer. By keeping the scripts elsewhere, those prefabs can be maintained, which can make the asset update game a little easier.

For us, in this book, we will be using a little bit of both methods. It really is easiest to get started by simply dropping a script on the object you want affected; but in the long run, the script holder that contains scripts does allow for some real benefits.

# A Note about This Approach

Through the course of these scripting tutorials, we will be looking at concepts realized through specific project-based efforts. Sometimes, this means we won't be using the absolutely most efficient method on our first pass since sometimes the most efficient methods are harder to understand. This means that sometimes we'll create a script and then later go back and optimize our approach as we learn more.

# Tools for Scripts

The following section describes some tools that are available for use with scripts.

# Editors

Unity itself does not edit scripts. Although you can view the contents of a script within Unity, the actual editing of the asset is done in some other application. On a Mac the included editor is Unitron. On the PC the included editor is UniSciTE. There are many other editors that could be used; really any basic text editor (Notepad for instance) can be used to edit scripts as they are just basic text. Some of the more sophisticated script editors (MonoDevelop, Unity Script Editor, or UnityDevelop) have some very elegant and powerful functionality built in to assist with scripting.

Both UniSciTE and unitron “understand” Unity's JavaScript, and thus will provide some visual clues about the script that is being written. Often this will include hints as simple as color coding recognized terms and can include suggestive options as the editor tries to guess what you mean. In these