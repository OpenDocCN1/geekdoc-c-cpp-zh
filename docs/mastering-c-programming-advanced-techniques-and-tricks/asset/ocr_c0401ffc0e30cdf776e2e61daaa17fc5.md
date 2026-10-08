# Example: Sanitizing Command-Line Input

Consider a C program that executes a system command based on user input. Without sanitization, this could lead to command injection attacks. The following example demonstrates how to sanitize such inputs.

```
#include #include #include void char *input) { char *allowedChars =
"ABCDEFGHIJKLMNOPQRSTUVWXYZabcdefghijklmnopqrstuvwxyz0123456789"; commandLength = strlen(command);
Sanitize input ( *input != '\0'; input++) { (strchr(allowedChars, *input))
{commandLength < sizeof(command) - 2) { = *input; '\0'; else
Execute sanitized command } int argc, char *argv[]) (argc != 2) {
argv[0])}; EXIT_FAILURE; EXIT_SUCCESS; }
```

This code safely appends user input to a predefined command string, ensuring that only alphanumeric characters are included. This approach effectively mitigates the risk of command injection attacks.

Output for input "Hello; rm -rf /\":
echo Hello"

In this example, potentially harmful input ("Hello; rm -rf /") is neutralized by only allowing specific, safe characters to be part of the command, thus preserving the security of the system while permitting a degree of user interaction.