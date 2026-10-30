# Privileges Required:

To manipulate content on the device or server requires the following privilege groups to be set:

| Privilege group | Privilege level | Description |
|---|---|---|
| LOCAL_CONTENT | NORMAL | Handling device content |
| CONTENT_TRANSFER | SYSTEM | Uploading and downloading content to and from a server |
| REMOTE_CONTENT | SYSTEM | Manipulating content on a server |

# Prerequisites:

To manipulate remote content developers will need an account on the bada Server. While the information about the remote content is stored on the bada Server, the physical content is stored on an Amazon S3 workspace, which you will need to set up and link to your application. You can set up the Amazon workspace from the Application Manager on the bada developer site, developer.bada.com, in the ‘Set Up Components’ section.

# Summary

Selected important classes:

+   - ContentInfo
+   - ContentManager
+   - ContentSearch

The Content namespace contains classes and methods that are used to search and manage content both locally on the device and remotely on the server. Content is the logical representation of various media types, including images, audio, and video, containing meta information such as date and time captured, GPS information, description, and the location of the actual content itself. This information can be used to search for content using an SQL-like syntax.

Creating, reading, updating, and deleting content is handled by the ContentManager and RemoteContentManager classes. Information in the content database on the device is accessed through specialised classes deriving from ContentInfo: AudioContentInfo, ImageContentInfo, and Video ContentInfo all of which contain information about their particular media types, while OtherContentInfo is used to represent content such as PDFs.

As shown in Figure 6.8, these classes are used to hold content information returned by these searches.