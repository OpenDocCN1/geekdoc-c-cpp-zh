# 29.11.13.37 Status known [fs.op.status.known]

```
bool status_known(file_status s) noexcept;
```

Returns: s.type() != file_type::none.

# 29.11.13.38 Symlink status [fs.op.symlink.status]

```
file_status symlink_status(const path& p);
file_status symlink_status(const path& p, error_code& ec) noexcept;
```

Effects: Same as status(), above, except that the attributes of p are determined as if by using POSIX lstat() to obtain a POSIX struct stat.

Let prms denote the result of (m & perms::mask), where m is determined as if by converting the st_mode member of the obtained struct stat to the type perms.

Returns: Same as status(), above, except that if the attributes indicate a symbolic link, as if by POSIX S_ISLNK, returns file_status(file_type::symlink, prms). The signature with argument ec returns file_status(file_type::none) if an error occurs.

Remarks: Pathname resolution terminates if p names a symbolic link.

Throws: As specified in 29.11.5.

# 29.11.13.39 Temporary directory path [fs.op.temp.dir.path]

```
path temp_directory_path();
path temp_directory_path(error_code& ec);
```

Let p be an unspecified directory path suitable for temporary files.

Effects: If exists(p) is false or is_directory(p) is false, an error is reported (29.11.5).

Returns: The path p. The signature with argument ec returns path() if an error occurs.

Throws: As specified in 29.11.5.

[Example 1: For POSIX-based operating systems, an implementation can return the path supplied by the first environment variable found in the list TMPDIR, TMP, TEMP, TEMPDIR, or if none of these are found, "/tmp".
For Windows-based operating systems, an implementation can return the path reported by the Windows GetTempPath API function. — end example]

# 29.11.13.40 Weakly canonical [fs.op.weakly.canonical]

```
path weakly_canonical(const path& p);
path weakly_canonical(const path& p, error_code& ec);
```

Returns: p with symlinks resolved and the result normalized (29.11.6.2).

Effects: Using status(p) or status(p, ec), respectively, to determine existence, return a path composed by operator/= from the result of calling canonical() with a path argument composed of the leading elements of p that exist, if any, followed by the elements of p that do not exist, if any. For the first form, canonical() is called without an error_code argument. For the second form, canonical() is called with ec as an error_code argument, and path() is returned at the first error occurrence, if any.

Postconditions: The returned path is in normal form (29.11.6.2).

Remarks: If a symbolic link is encountered during pathname resolution, pathname resolution continues using the contents of the symbolic link.

Otherwise, if the attributes indicate a socket, as if by POSIX S_ISSOCK, returns file_status(file_type::socket, prms).

Otherwise, if the attributes indicate an implementation-defined file type (29.11.8.2), returns file_status(file_type::A, prms), where A is the constant for the implementation-defined file type.

Otherwise, returns file_status(file_type::unknown, prms).