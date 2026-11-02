
Such launching happens through the Windows Explorer on the desktop or programmatically through WinRT APIs in `Windows.System.Launcher`. In either case, the associated app gets activated with an activation kind of `File`, and the activation event args will contain the appropriate `StorageFile` objects. We'll see the details toward the end of this chapter.

### Sidebar: Enterprise File Protection

There is an additional set of capabilities with the file system that are not covered in this book, namely the `Windows.Security.EnterpriseData.FileRevocationManager` APIs. These help you manage copy protection for any `StorageItem` with what is called *selective wipe*, which is described in the [Security documentation](). This accommodates enterprise users that bring their own mobile devices to work and use them to access corporate data. IT departments, of course, want to make sure that such data doesn't get leaked outside the enterprise environment. Access to files and folders, then, can be granted in a protected manner through `FileRevocationManager.ProtectAsync` such that they can be revoked remotely through a server-issued command. Revoked files are completely inaccessible even though they still technically exist on the file system.

For use of the API, refer to the [File Revocation Manager sample]().

## Using the File Picker and Access Cache

Although the File Picker doesn't sound all that glamorous, it's actually, to my mind, one of the coolest features in Windows. “Wait a minute!” you say, “How can a UI to pick a file or folder be, well, cool?” The reason is that *this is the place* where the users can browse and select from their entire world of data. That world—as I've said several times already—includes locations well beyond what we normally think of as the local file system (local drives, removable drives, and the local network). Those added locations are made available by what are called *file picker providers*: apps that specifically take a library of data that's otherwise buried behind a web service, within an app's own database, or even generated on the fly, and makes it appear as if it's part of the local file system.

Think about this for a moment (as I invited you to do way back in Chapter 1, “The Life Story of a Windows Store App”). When you want to work with an image from a photo service like Flickr or Picasa, for example, what do you typically have to do? First step is to download that file to the local file system within some app that gives you an interface to that service (which might be a web app). Then you can make whatever edits and modifications you want, after which you typically need to upload the file back to the service. Well, that's not so bad, except that it's time consuming, it forces you to switch between multiple apps, and eventually it litters your system with a bunch of temporary files, the relationship of which to your online service is quickly forgotten.

Having a file picker provider that can surface such data directly, both for reading and writing, eliminates all those intermediate steps and eliminates the need to switch apps. This means that a provider for a photo service makes it possible for other apps to load, edit, and save online content as if it all existed on the local file system. Consuming apps don't need to know anything about those other services, and they automatically have access to more services as more provider apps are installed. What's more, providers can also make data that's not normally stored as files appear as though they are. For example, the Sound Recorder app that's built into Windows is a file picker provider that lets you record a new audio file and return it just as if it had already been present on the file system. All of this gives users a very natural means to flow in and out of data no matter where it's stored. Like I said, I think this is a very cool feature!

In this section, we'll first look at the file picker UI so that we know what's going to appear when we use the file picker API in `Windows.Storage.Pickers`. Then we'll see the `Windows.Storage.AccessCache` API, because it's in the context of the file picker that you'll typically be saving file permissions for later sessions.

We'll look more at the question of providers in Appendix D, "Contract Providers." Our more immediate concern is how to use these file pickers to obtain a `StorageFile` or `StorageFolder` object.

### The File Picker UI

When a file picker is invoked, you'll see a full-screen view like that in Figure 11-3, depending on whether you want single or multiple selection, whether you're picking files or folders (or a save location), and whether you want only specific file types. In the case of Figure 11-3, the picker is invoked to choose a single image with a thumbnail view (which provides a rich tooltip control when you hover over an item). In a way, the file picker itself is like an app that's invoked for this purpose, and it's designed (with a black background) to give full attention to the contents of the files. The pickers also provide semantic zoom capabilities, as you'd expect, and can be invoked in any sized view even down to the 320px minimum, as shown on the right of the figure.

![](img/0e8e4a2b6f953d3397e14e88cd5d8b4d_563_0.png)

**FIGURE 11-3** A single-selection file picker on the Pictures library in thumbnail view mode, with a hover tooltip showing for one of the items (the head of the Sphinx) and the selection frame showing on another (the Taj Mahal). The overlay on the right shows the file picker in a narrow 320px view. Bonus points if you can identify the location of the other runs in the main view on the left! (And if you're wondering, these are all my own photos.)

In Figure 11-3, the Pictures heading shows the current location of the picker. The Sort By Name drop-down lets you choose other sorting criteria, and the This PC header is also a drop-down list that lets you navigate to different locations, as shown in Figure 11-4, including other areas of the file system (though never protected areas like the Windows folder or Program Files), network locations, and other provider apps. When choosing a picture (left side), notice how the list of apps is filtered to show just those that can provide pictures; when choosing general files or other types like music (right side), additional apps like the Sound Recorder can appear.

![](img/0e8e4a2b6f953d3397e14e88cd5d8b4d_564_0.png)

**FIGURE 11-4** Selecting other picker locations, notice that SkyDrive and apps are listed along with file system locations. The picker on the left is invoked to select pictures, so only picture-providing apps appear; the picker on the right is invoked to select any type of file, so additional providers appear.

Choosing another file system or network location navigates there, of course, from which you can browse into other folders. As SkyDrive is built into Windows, it's effectively treated like another network location, as shown in Figure 11-5, and it's also the default location for the file saver picker (controlled through PC Settings > SkyDrive > File Storage > Save Documents to SkyDrive by Default).

![](img/0e8e4a2b6f953d3397e14e88cd5d8b4d_564_1.png)

**FIGURE 11-5** When picking files from SkyDrive, your cloud storage appears like any other local or network location.

Selecting an app, on the other hand, launches that app through the file picker provider contract. In this case it appears within a system-provided—but app-branded—UI like that shown in Figure 11-6.

In Figure 11-3, Figure 11-5, and Figure 11-6, the picker is invoked to select a single file. In Figure 11-7, on the other hand, it is invoked to select multiple files—which can again come from the file system, network or cloud locations, or other apps—it doesn't matter! With multiple selection, selected items are placed into what's called the *basket* on the bottom of the screen. You can see this in Figure 11-7 and also in Figure 11-8 (where the picker is using list view mode rather than thumbnails). The purpose of the basket is to let you select items from one location, navigate to a new location through the header drop-down, select a few more, and then navigate to still other locations. In short, the basket holds whatever items you select from *wherever locations*. The basket in Figure 11-8 contains the sound recording from Figure 11-7, a picture from my phone, a picture from SkyDrive, an MP3 file from my Music folder, and a couple videos from the current folder.

![](img/0e8e4a2b6f953d3397e14e88cd5d8b4d_566_0.png)

**FIGURE 11-8** The file picker in multiselect mode with the selection basket at the bottom. The picker's layout here is a "list" view mode (not thumbnails) that's set independently from the selection mode.

The picker can also be used to select a folder, as shown in Figure 11-9 (provider apps aren't shown from the heading drop-down in this case), or a save location and filename, as shown in Figure 11-10.
