
## 5.2. std::string 参考

- `string::iterator begin():`

  返回一个指向当前 string 对象第一个字符的迭代器。对于 `const` string 对象，返回 `const_iterator`。

- `size_type capacity() const:`

  返回当前 string 对象无需调整大小即可存储的字符数。

- `int compare(string const &argument) const:`

  使用 ASCII 字符排序序列，对当前 string 对象中存储的文本与 argument 中存储的文本进行字典序比较。如果两个字符串内容相同，则返回 0；如果当前对象中的文本应排在 argument 中的文本之前，则返回负值；如果当前对象中的文本应排在 argument 中的文本之后，则返回正值。

- `int compare(size_t opos, size_t on, string const &argument) const:`

  将当前 string 对象中存储文本的一个子字符串与 argument 中存储的文本进行比较。从偏移 opos 开始的最多 on 个字符会与 argument 中的文本进行比较。

- `int compare(size_t opos, size_t on, string const &argument, size_type apos, size_type an) const:`

  将当前 string 对象中存储文本的一个子字符串与 argument 中存储文本的一个子字符串进行比较。当前 string 对象中从偏移 opos 开始的最多 on 个字符，会与 argument 中从偏移 apos 开始的最多 an 个字符进行比较。在这种情况下，argument *必须* 是 string 对象。

- `int compare(size_t opos, size_t on, char const *argument, size_t an):`

  将当前 string 对象中存储文本的一个子字符串与 argument 中存储文本的一个子字符串进行比较。当前 string 对象中从偏移 opos 开始的最多 on 个字符，会与 argument 中最多 an 个字符进行比较。argument 必须至少包含 an 个字符。这些字符可以具有任意值：ASCII-Z 值没有特殊含义。

- `size_t copy(char *argument, size_t on, size_type opos) const:`

  当前 string 对象的内容被（部分）复制到 argument 中。返回实际复制的字符数。第二个参数指定要从当前 string 对象复制的字符数，是必需的。复制后的字符串不会追加 ASCII-Z，但可以使用如下惯用法将 ASCII-Z 追加到复制文本中：

  ```cpp
  argument[object.copy(argument, string::npos)] = 0;
  ```

  当然，程序员应确保 argument 的大小足以容纳额外的 0 字节。

- `char const *c_str() const:`

  当前 string 对象的内容以 ASCII-Z 结尾的 C 字符串形式返回。

- `char const *data() const:`

  返回当前 string 对象的原始内容。由于该成员不返回以 ASCII-Z 结尾的 C 字符串（不像 c_str 那样），因此它可用于检索当前 string 对象内部存储的任何类型的信息，例如一系列 0 字节：

  ```cpp
  string s(2, 0);
  cout << static_cast<int>(s.data()[1]) << '\n';
  ```

- `bool empty() const:`

  如果当前 string 对象不包含数据，则返回 `true`。

- `string::iterator end():`

  返回一个指向当前 string 对象最后一个字符之后位置的迭代器。对于 `const` string 对象，返回 `const_iterator`。

- `string &erase(size_type opos, size_type on):`

  删除当前 string 对象中存储信息的一个（子）字符串。

- `string::iterator erase(string::iterator begin, string::iterator end):`

  参数 end 是可选的。如果省略，则使用当前对象的 end 成员返回的值。删除由 begin 和 end 迭代器定义的字符。返回迭代器 begin，此时它指向最后一个被删除字符之后的位置。

- `size_t find(string const &argument, size_type opos) const:`

  返回当前 string 对象中找到 argument 的第一个索引。

- `size_t find(char const *argument, size_type opos, size_type an) const:`

  返回当前 string 对象中找到 argument 的第一个索引。当指定全部三个参数时，第一个参数必须是 `char const *`。

- `size_t find(char ch, size_type opos) const:`

  返回当前 string 对象中找到 ch 的第一个索引。

- `size_t find_first_of(string const &argument, size_type opos) const:`

  返回当前 string 对象中第一个找到 argument 中任意字符的索引。

- `size_type find_first_of(char const *argument, size_type opos, size_type an) const:`

  返回当前 string 对象中第一个找到 argument 中任意字符的索引。如果提供 opos，它指的是当前 string 对象中应开始搜索 argument 的第一个索引。如果省略，则完整扫描 string 对象。如果提供 an，它表示搜索中应使用的 `char const *` 参数中的字符数。它定义从 argument 开头开始的子字符串。如果省略，则使用 argument 的所有字符。

- `size_type find_first_of(char ch, size_type opos) const:`

  返回当前 string 对象中找到字符 ch 的第一个索引。

- `size_t find_first_not_of(char ch, size_type opos) const:`

  返回当前 string 对象中第一个找到不同于 ch 的字符的索引。

- `size_t find_last_of(string const &argument, size_type opos) const:`

  返回当前 string 对象中最后一个找到 argument 中任意字符的索引。

- `size_type find_last_of(char const *argument, size_type opos, size_type an) const:`

  返回当前 string 对象中最后一个找到 argument 中任意字符的索引。如果提供 opos，它指的是当前 string 对象中应开始搜索 argument 的最后一个索引。如果省略，则完整扫描 string 对象。如果提供 an，它表示搜索中应使用的 `char const *` 参数中的字符数。它定义从 argument 开头开始的子字符串。如果省略，则使用 argument 的所有字符。

- `size_type find_last_of(char ch, size_type opos) const:`

  返回当前 string 对象中最后一个找到字符 ch 的索引。

- `size_t find_last_not_of(string const &argument, size_type opos) const:`

  返回当前 string 对象中最后一个找到未出现在 argument 中的任意字符的索引。

- `istream &std::getline(istream &istr, string &object, char delimiter = '\n'):`

  注意：这不是 string 类的成员函数。

  从 istr 读取一行文本。从 istr 读取直到 delimiter（或流末尾，以先出现者为准）的所有字符，并存储到 object 中。如果遇到 delimiter，则将其从流中移除，但不存储到 object 中。

  如果未找到 delimiter，则 istr.eof 返回 true（参见第 6.3.1 节）。由于流可被解释为 bool 值（参见第 6.3.1 节），一种常见的惯用法是将流中的所有行依次读入 string 对象 line，如下所示：

  ```cpp
  while (getline(istr, line))
      process(line);
  ```

  最后一行的内容，无论是否以 delimiter 结束，最终也会赋给 object。

- `string &insert(size_t opos, string const &argument, size_type apos, size_type an):`

  argument 的一个（子）字符串插入到当前 string 对象的索引位置 opos 处。apos 和 an 参数必须同时提供，或者同时省略。

- `string &insert(size_t opos, char const *argument, size_type an):`

  argument（类型为 char const *）插入到当前 string 对象的索引 opos 处。

- `string &insert(size_t opos, size_t count, char ch):`

  将 count 个字符 ch 插入到当前 string 对象的索引 opos 处。

- `string::iterator insert(string::iterator begin, char ch):`

  字符 ch 插入到由 begin 引用的当前对象位置。返回 begin。

- `string::iterator insert(string::iterator begin, size_t count, char ch):`

  将 count 个字符 ch 插入到由 begin 引用的当前对象位置。返回 begin。

- `string::iterator insert(string::iterator begin, InputIterator abegin, InputIterator aend):`

  由 InputIterator abegin 和 aend 定义的范围内的字符插入到由 begin 引用的当前对象位置。返回 begin。

- `size_t length() const:`

  返回当前 string 对象中存储的字符数。

- `size_t max_size() const:`

  返回当前 string 对象中可存储的最大字符数。
