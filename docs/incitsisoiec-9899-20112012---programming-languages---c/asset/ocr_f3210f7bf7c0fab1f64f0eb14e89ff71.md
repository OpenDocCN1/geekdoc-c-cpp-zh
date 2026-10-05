# H.3 Notification

Notification is the process by which a user or program is informed that an exceptional arithmetic operation has occurred. C's operations are compatible with LIA–1 in that C allows an implementation to create a notification to occur when any arithmetic operation returns an exceptional value as defined in LIA–1 clause 5.

# H.3.1 Notification alternatives

+   LIA–1 requires at least the following two alternatives for handling of notifications: setting indicators or trap-and-terminate. LIA–1 allows a third alternative: trap-and-resume.

+   An implementation need only support a given notification alternative for the entire program. An implementation may support the ability to switch between notification alternatives during execution, but is not required to do so. An implementation can provide separate selection for each kind of notification, but this is not required.

+   C allows an implementation to provide notification. C's SIGFPE (for traps) and FE_INVALID, FE_DIVBYZERO, FE_OVERFLOW, FE_UNDERFLOW (for indicators) can provide LIA–1 notification.

+   Cs signal handlers are compatible with LIA–1. Default handling of SIGFPE can provide trap-and-terminate behavior, except for those LIA–1 operations implemented by math library function calls. User-provided signal handlers for SIGFPE allow for trap-and-resume behavior with the same constraint.

# H.3.1.1 Indicators

+   C's <fenv.h> status flags are compatible with the LIA–1 indicators.

+   The following mapping is for floating-point types:

undefined FE_INVALID, FE_DIVBYZERO
floating_overflow FE_OVERFLOW
underflow FE_UNDERFLOW

+   The floating-point indicator interrogation and manipulation operations are:

set_indicators feraisecept (i)
clear_indicators flecleareexcept (i)
test_indicators fetestexcept (i)
current_indicators fetestexcept (FE_ALL_EXCEPT)

where i is an expression of type int representing a subset of the LIA–1 indicators.