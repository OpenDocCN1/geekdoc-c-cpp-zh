# Table 29.1: Showing the Classes of the System.IO namespace

| Class | Description |
|---|---|
| FileNotFoundException | Raises an exception when you attempt to access the file that does not exist in the hard-disk. |
| FileStream | Exposes the stream around the file that supports both synchronous and asynchronous read and write operations. |
| FileSystemInfo | Provides the base class information for both the FileInfo and DirectoryInfo objects. |
| StreamReader | Implements a TextReader object that helps in reading characters from a byte stream using a certain specific encoding, such as UTF-8 and UTF-16. |
| StreamWriter | Implements a TextWriter object that helps in writing characters to a stream using a certain specific encoding, such as UTF-8 and UTF-16. |

After exploring the important classes of the System.IO namespace, let’s now learn how to work with drives.

# Working with Drives

Before we start exploring drives in C#, let’s first examine few terms that are quite often used while working with drives. A list of some of these terms is given as follows:

+   - Drive letter — Represents the name provided by a user to the different logical drives of a system. To provide the name to a drive, you can use the Name property. This property helps you provide alphabetical identifiers, such as C:\, D:\, and E:\, to drives.
+   - Drive state — Specifies the state of a drive, such as whether the drive is in the ready state or not. You can use the IsReady property to determine the state of a drive. If you query a drive that is not in the ready state, an exception occurs.
+   - Drive type — Refers to the type of drive that is attached with your system. You can use the DriveType property to determine the type of drive. A drive can be of the CD-ROM, FIXED, UNKNOWN, NETWORK, NOROOTDIRECTORY, Random Access Memory (RAM), or REMOVABLE type. The values for all these types are specified in the DriveType enumeration. This enumeration defines the constants for drive types. Different members of the DriveType enumeration are as follows:
+     - Unknown — Represents an unknown drive type
+     - NoRootDirectory — Represents a drive that does not have a root directory
+     - Removable — Represents a drive that is removable in nature, such as Floppy Disk Drive or Universal Serial Bus (USB) Flash Drive
+     - Fixed — Represents a drive that is a fixed disk, and cannot be removed
+     - Network — Represents a drive that is accessed through network
+     - CD-ROM — Represents a drive that is optical in nature, such as CD or DVD ROM
+     - RAM — Represents a drive that is Random Access Memory (RAM) disk
+   - Volume label — Helps in setting or retrieving the name of a drive. The length of the label is based on the type of operating system. For example, New Technology File System (NTFS) allows a volume label of up to 32 characters long. You can set a volume label of a drive with the help of the VolumeLabel property of the DriveInfo class. Note that if you enter Null as your drives volume label, no exception occurs because the VolumeLabel property allows Null values.
+   - File system format — Specifies the name of the file system provided to a drive, such as NTFS or FAT. NTFS is the most standard file system of Windows NT. It is supported by all the later versions of Windows, such as Windows 2000, Windows XP, Windows Server 2003, and Windows Vista. On the other hand, the FAT file system is supported by almost all the existing operating systems, mainly the computers for personal usage.