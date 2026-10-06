# ISO/IEC 14882:2017(E)

(6.4) Filenames that have special meaning.

(6.5) Awareness and sensitivity during path resolution.

(6.6) Special rules that apply to file types other than regular files, such as directories.

A hard link to an existing file. Some file systems support multiple hard links to a file. If the last hard link to a file is removed, the file itself is removed. [Note: A hard link can be thought of as a shared-ownership pointer to a file.] — end note

A link is an object that associates with a file. Several links can associate with the same file.

The native encoding of a character string is the operating system dependent current encoding for patenames. The native encoding for wide character strings is the implementation-dependent execution wide-character set encoding (5.3).

The native format is the operating system dependent pathname format accepted by the host operating system.

Normalization of a generic pathname means:

+   1. If the path is empty,

+   2. Replace each slash-separator with a preferred-separator.

+   3. Replace each directory-separator as a preferred-separator. [Note: The generic grammar (30.10.8.1) defines directory-separator as one or more separators and preferred-separators.] — end note

+   4. Remove each dot-directory and immediately following directory-separator.

+   5. As long as any path exists, remove a dot-dot immediately followed by a directory-separator and a dot-dot, along with any immediately following directory-separator.

+   6. If there is a root-directory, remove all dot-dot filenames and any directory-separators following them. [Note: These dot-dot filenames attempt to reference nonexistent parent directories.] — end note

+   7. If the last component is dot-dot, remove any trailing directory-separator.

+   8. If the path is empty,

The result of normalization is a path in normal form, which is said to be normalized.

Operating system dependent behavior that is dependent on the behavior and characteristics of an operating system. 30.10.2.2.

The parent directory of a directory is the directory that contains a entry for the given directory and is represented by the dot-dot in the file. The parent directory of other types of files is a directory containing a directory entry for the file under discussion.

A sequence of elements that identify the location of a file within a filesystem. The elements are the root-name, directory-separator, and an optional sequence of filenames. The maximum number of elements in the sequence is operating system dependent.

A pathname is a character string that represents the name of a path. Patenames are formatted according to the generic pathname grammar (30.10.8.1) or an operating system dependent native pathname format.

Pathname resolution is the operating system dependent mechanism for resolving a pathname to a file in a hierarchy. There may be multiple paths that resolve to the same file. [Example: POSIX specifies the mechanism in section 4.1, Pathname resolution.] — end example

A relative path is a path that is not absolute, and so, uniquely identifies the location of a file when resolved relative to an implied starting location. The elements of a path that determine if it is