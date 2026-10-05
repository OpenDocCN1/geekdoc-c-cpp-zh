arbitrarily. There are also a few things you need to consider:

+   * Numeric types
When reading a numeric value, the input must start with at least one digit. If you specify the sign with + or -, it must only appear before the first digit. However, there must be no space between the sign and the digit. Leading whitespace characters are ignored. In case of an erroneous input, the numeric value is set to 0 and std::failbit is set.

+   * char*
The use of char* for input was already critical in C. Input is read until the first whitespace or end of file (EOF; more on this later). Leading whitespace is skipped, which can be changed with the cinws manipulator. The problem with reading char* is that it can read beyond the buffer area (buffer overflow)—for example, char cval[20];std::cin >> cval. If you read in more than 20 characters here, cin will duly do so and write into an undefined memory area. Therefore, with old C-strings (if you absolutely must use them), you must always ensure the maximum length is not exceeded. For this, the setw manipulator is suitable—for example, cin >> setw(20) >> cval.

+   * bool
The output of bool is converted to 0 for false and 1 for true. The same rules as for numeric values apply initially. When entering valid numeric values other than 0, it is converted to 1 (= true). When