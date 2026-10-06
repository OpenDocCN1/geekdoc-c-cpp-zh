# ISO/IEC 14882:2017(E)

(6.1.2) Otherwise, if the specific error indicates that p can be resolved then the attributes cannot be determined, returns file_status(file_type::unknown).

(6.1.3) Otherwise, returns file_status(file_type::none).

[Note: These semantics distinguish between p known not to exist, p existing but not being able to determine its attributes, and there is an error that prevents even if p exists. These distinctions are important to use cases. -- end note]

(6.2) Otherwise,

(6.2.1) If the attributes indicate a regular file, as by POSIX S_REG, returns file_status(file_type::regular, prms). [Note: file_type::regular implies appropriate <stream> operations would succeed, assuming no hardware, permission, or file system errors. Lack of file_type does not necessarily imply <stream> operations would fail in a directory. -- end note]

(6.2.2) Otherwise, if the attributes indicate a directory, as by POSIX S_ISDIR, returns file_status(file_type::directory, prms). -- end note]

(6.2.3) Otherwise, if the attributes indicate a special file, as by POSIX S_ISBLK, returns file_status(file_type::block, prms).

(6.2.4) Otherwise, if the attributes indicate a character file special, as by POSIX S_ISCHR, returns file_status(file_type::character, prms).

(6.2.5) Otherwise, if the attributes indicate a pipe or fifo file, as by POSIX S_IFIFO, returns file_status(file_type::fifo, prms).

(6.2.6) Otherwise, if the attributes indicate a socket, as by POSIX S_ISSOCK, returns file_status(file_type::socket, prms).

(6.2.7) Otherwise, if the attributes indicate an implementation-defined type (type 30.10.10), returns file_status(file_type::_A, prms).

(6.2.8) Otherwise, returns file_status(file_type::unknown, prms).

7 Remarks: If a symbolic link is encountered during pathname resolution, pathname resolution continues using the contents of the symbolic link.

# 30.10.15.36 Status known

```
bool file_status(file_status s) noexcept
Returns: s.type() == file_type::none;
```

# 30.10.15.37 Symbolic link

```
file_symlink_status(const path& p, error_code& ec) noexcept
```

Effects: Same as status(), above, except that the attributes of p are determined as if using POSIX stat() to obtain a POSIX struct.

2 Let prms denote the result of (m & mask); where m is determined as by converting the st_mode of the obtained struct to type prms.

3 Returns: Same as status(), above, except that the attributes indicate a symbolic link, as if by POSIX S_ISLNK, returns file_status(file_type::symlink, prms). The signature with argument ec returns file_status(file_type::none) if an error occurs.