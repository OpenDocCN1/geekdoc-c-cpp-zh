# Softkey Template and Phone Button Template

The Softkey Template controls softkey button functions are available to the user; these are typically used for feature access (Conference, Transfer, Park, Extension Mobility, and so on). Seven softkey templates are available by default, and you can create as many as your design requires.

The Phone Button Template defines the behavior of the buttons to the right of the phone screen (for most models). Eighty (or more) are defined by default, because there are unique templates for each supported phone type—and for most phones, a separate template for SCCP and SIP. The default templates typically provide two lines and as many speed dials as there are remaining buttons on a particular phone model; you can add and customize each button one of many different functions.

# Profiles

Profiles allow for a one-time configuration of repetitive tasks; several types of profiles exist, and you can create many versions of each type to be applied to phones as needed.

# Phone Security Profile

A default Phone Security Profile exists for each type of phone/protocol. These default profiles have security security disabled; you can choose to configure the device as secured, set encrypted TFTP configuration files, and modify Certificate Authority Proxy settings.

# Common Phone Profile

The Common Phone Profile includes settings that control the behavior of the phone, including the following:

+   - DND settings
- Phone personalization capabilities
- VPN settings
- USB port behavior
- Video capabilities
- Power-save options

# Adding Phones in CUCM

Phones can be added to CUCM in four ways:

+   - Manual Configuration: The administrator creates a new phone, configuring all settings in real time on the Phone Configuration page.
- Autoreistration: The administrator configures CUCM to dynamically configure and add to the database any new IP Phone that connects to the network.