+   - Serviceability
- OS Administration
- Disaster Recovery System
- Cisco Extension Mobility
- Cisco Unified Communications Manager Assistant
- Directories

+   - IP Phone Services
- Data Associated with User Accounts

User account information is divided into three categories, with fields for specific data in each category:

# 1. Personal and Organizational Settings:

+   - UserID
- First, Middle, Last Name
- Manager UserID
- Department
- Phone Number, Mail ID

# 2. Password Information:

+   - Password

# 3. CUCM Configuration Settings:

+   - PIN
- SIP Digest Credentials
- User Groups and Roles
- Associated PCs, controlled devices, and DNs
- Application and feature parameters (Extension Mobility, Presence Group, CAPF)

Application User accounts use a subset of the previous attributes.

# User Locale

User locales allow different languages to be displayed on the IP Phone and the User Web Pages. Additional locales are installed on the CUCM server; then specific locale files are downloaded to the phone via TFTP. This allows for the customization of the primary interfaces for users in a wide range of available locales/languages.

# Device Association

For users to be able to control their own devices (setting up their speed dials, services, and ring preferences, for example), the End User account must be associated with the