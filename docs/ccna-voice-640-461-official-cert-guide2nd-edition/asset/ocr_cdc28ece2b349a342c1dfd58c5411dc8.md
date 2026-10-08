Date/Time Group As discussed earlier, it is recommended to use NTP for time synchronization of all devices. The problem is that NTP references Greenwich Mean Time, which makes the time displayed on devices "wrong" if they are not in the GMT time zone. Date/Time Groups allow us to offset the correct time learned via NTP to match the time zone of the device. Date/Time Groups also allow us to display the time and date in the desired format, which can vary from place to place.

Phone NTP Reference needs an NTP server address from which they can obtain the time using NTP. (This is not required for SCCP phones, which are configured to use the correct time using SCCP signaling.) It is preferred that the NTP reference be local to the phones that need it.

It is common to have groups of phones with similar configurations. Using a Device Pool for each group simplifies and speeds up administrative tasks, making them less error-prone in the bargain. Figure 9-4 shows part of a Device Pool configuration.

![](bbox=[0.249, 0.178, 0.663, 0.822])

### Figure 9-4 Device Pool

# Device Defaults

The Device Defaults page lists all the supported endpoints (with separate entries for SCCP and SIP as necessary), and the firmware load, Device Pool, and Phone Button Template each endpoint uses by default. This allows an administrator to set useful system-wide defaults for any newly registered device of each type.