# ISO/IEC 14882:2017(E)

```
bool is_character_file(const path& p);
bool is_character_file(const path& p, error_code& ec) noexcept;

bool is_directory(file_status s) noexcept;
bool is_directory(const path& p);
bool is_directory(const path& p, error_code& ec) noexcept;

bool is_empty(const path& p);
bool is_empty(const path& p, error_code& ec) noexcept;

bool is_fifo(file_status s) noexcept;
bool is_fifo(const path& p);
bool is_fifo(const path& p, error_code& ec) noexcept;

bool is_other(file_status s) noexcept;
bool is_other(const path& p);
bool is_other(const path& p, error_code& ec) noexcept;

bool is_regular(file_status s) noexcept;
bool is_regular(const path& p);
bool is_regular(const path& p, error_code& ec) noexcept;

bool is_socket(file_status s) noexcept;
bool is_socket(const path& p);
bool is_socket(const path& p, error_code& ec) noexcept;

bool is_symlink(file_status s) noexcept;
bool is_symlink(const path& p);
bool is_symlink(const path& p, error_code& ec) noexcept;

file_type last_write_time(const path& p);
void file_type last_write_time(const path& p, error_code& ec) noexcept;
void last_write_time(const path& p, file_type new_time, error_code& ec) noexcept;

boid permissions(const path& p, perms perms, perm_options opts=perm_options::replace);
boid permissions(const path& p, perms perms, error_code& ec) noexcept;
boid permissions(const path& p, perms perms, perm_options opts, error_code& ec) noexcept;

path proxyate(const path& p, error_code& ec = {}););
path proxyate(const path& p, const path& base = current_path());
path proxyate(const path& p, const path& base, error_code& ec);

path read_symlink(const path& p);
path read_symlink(const path& p, error_code& ec) noexcept;

path relative(const path& p, error_code& ec);
path relative(const path& p, const path& base = current_path());
path relative(const path& p, const path& base, error_code& ec);

bool remove(const path& p);
bool remove(const path& p, error_code& ec) noexcept;

uintmax_t remove_all(const path& p);
```