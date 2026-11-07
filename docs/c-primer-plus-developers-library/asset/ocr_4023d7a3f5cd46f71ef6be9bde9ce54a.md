![](bbox=[0.13, 0.1, 0.84, 0.38])

Figure 17.6 Some file-opening modes.

# Table 17.8 C++ and C File-Opening Modes

| C++ mode | C mode | Meaning |
| --- | --- | --- |
| `ios_base::in` | `"r"` | Open for reading. |
| `ios_base::out` | `"w"` | (Same as `ios_base::out \| ios_base::trunc`.) |
| `ios_base::out \| ios_base::trunc` | `"w"` | Open for writing, truncating file if it already exists. |
| `ios_base::app` | `"a"` | Open for writing, append only. |
| `ios_base::in \| ios_base::out` | `"r+"` | Open for reading and writing, with writing permitted anywhere in the file. |
| `ios_base::in \| ios_base::out \| ios_base::trunc` | `"w+"` | Open for reading and writing, first truncating file if it already exists. |
| `c++mode \| ios_base::binary` | `"cmodeb"` | Open in `c++mode` or corresponding `cmode` and in binary mode; for example, `ios_base::in \| ios_base::binary` becomes `"rb"`. |
| `c++mode \| ios_base::ate` | `"cmode"` | Open in indicated mode and go to end of file. C uses a separate function call instead of a mode code. For example, `ios_base::in \| ios_base::ate` translates to the `"r"` mode and the C function call `fseek(file, 0, SEEK_END)`. |