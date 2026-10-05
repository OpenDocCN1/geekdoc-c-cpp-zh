# Description

4 The fopen_s opens the file whose name is the string pointed to by filename, and associates a stream as described for fopen, with the addition that modes starting with

5 The mode string shall be with the character 'w' or 'a' may be preceded by the character 'u', see below:


+   - uw truncate to zero length or create text file for writing, default permissions
- uwx create text file for writing, default permissions
- ua append; open or create text file for writing at end-of-file, default permissions
- uwb truncate to zero length or create binary file for writing, default permissions
- ubwx create binary file for writing, default permissions
- uab append; open or create binary file for writing at end-of-file, default permissions
- uw+ truncate to zero length or create text file for update, default permissions
- uw+x create text file for update, default permissions
- ua+ append; open or create text file for update, writing at end-of-file, default permissions
- uw+b or uw+b truncate to zero length or create binary file for update, default permissions
- uw+bx or uw+bx create binary file for update, default permissions
- ua+ or uab+ append; open or create binary file for update, writing at end-of-file, default permissions

6 Opening a file with exclusive mode ('x' as the last character in the mode argument) fails if the file already exists or cannot be created.

7 To the extent that the underlying system supports the concepts, files opened for writing shall be opened with exclusive (also known as non-shared) access. If the file is created, and the first character of the mode string is not 'u', to the extent that the underlying system supports it, the file shall have a file permission that prevents other users on the system from accessing the file. If the file is being created and first character of the mode string is 'u', then by the time the file has been closed, it shall have the system default access permissions.(389)

8 If the file was opened successfully, then the pointer to FILE pointed by streamptr will be set to the pointer to the object controlling the opened file. Otherwise, the pointer