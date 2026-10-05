users can add their own error groups or recognize those defined by the system.

The <system_error> header primarily 28.5.1 Overview defines the following components:

+   * class error_code
Represents a (system-)specific error value that can be returned by an operation, such as a system function call.

+   * class error_condition
A generic error condition against which one checks in their portable code.

+   * class error_category
Classification of errors into groups/families, also an abstract base class for translation into readable text.

+   * class system_error
Is an exception class that contains an error_code when an error is propagated by exception.

+   * enum class errc
Is an enumeration of general-purpose values derived from the POSIX standard of type error_condition.

+   * is_error_code_enum<>, is_error_condition_enum<,
make_error_code, make_error_condition
Implement mechanisms to convert enum class values into error_condition values.

+   * generic_category()
Returns an error_category instance that can interpret errc-based codes and conditions.