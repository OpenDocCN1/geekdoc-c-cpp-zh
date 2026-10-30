# Table R1.2 (continued)

| Error code | Description |
|---|---|
| E_UNDERFLOW | The operation causes an underflow |
| E_UNKNOWN | An unknown error has occurred |
| E_UNSUPPORTED_ALGORITHM | The specified algorithm is not supported |
| E_UNSUPPORTED_CODEC | The required CODEC is not found |
| E_UNSUPPORTED_FAMILY | The requested address family is not supported |
| E_UNSUPPORTED_FORMAT | The current implementation does not support the format of the input |
| E_UNSUPPORTED_PROTOCOL | The specified protocol is not supported |
| E_UNSUPPORTED_OPERATION | The current implementation does not support the requested operation |
| E_UNSUPPORTED_OPTION | The specified option is not supported |
| E_UNSUPPORTED_SERVICE | The specified service is not supported |
| E_UNSUPPORTED_TYPE | The specified type is not supported |
| E_USER_AGENT_NOT_ALLOWED | Used by an HTTP transaction |
| E_USER_ALREADY_REGISTERED | The user is already registered to the device |
| E_USER_NOT_FOUND | The required user does not exist |
| E_USER_NOT_REGISTERED | No user is registered to the device yet |
| E_WOULD_BLOCK | A non-blocking socket operation could not be completed immediately |

# Recipe 1.3: Use Two-phase Construction and Leak-free Destruction

# Problem Description

You want to construct bada objects by using the two-phase construction mechanism in order to avoid memory leaks.

# The Recipe

The following configuration is required for this recipe: