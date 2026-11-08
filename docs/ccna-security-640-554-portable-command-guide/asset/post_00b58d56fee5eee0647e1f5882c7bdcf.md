
- Data Plane Security 37
  - ACLs 37
  - Antispoofing 38
  - Layer 2 Data Plane Protection 38

## CHAPTER 5 Protecting the Network Infrastructure Using CCP 39

- Cisco Configuration Professional 39
- Cisco Configuration Professional Express 40
  - Connecting to Cisco CP Express Using the GUI 41
- Cisco Configuration Professional 44
  - Configuring an ISR for CCP Support 44
  - Installing CCP on a Windows PC 45
  - Connecting to an ISR Using CCP 45
- CCP Features and User Interface 47
  - Application Menu Options 48
  - Toolbar Menu Options 48
  - Toolbar Configure Options 49
  - Toolbar Monitor Options 49
- Using CCP to Configure IOS Device-Hardening Features 49
  - CCP Security Audit 49
  - CCP One-Step Lockdown 50
- Using the Cisco IOS AutoSecure CLI Feature 51
  - Configuring AutoSecure via the CLI 51

## CHAPTER 6 Securing the Management Plane 53

- Planning a Secure Management and Reporting Strategy 54
- Securing the Management Plane 54
  - Securing Passwords 55
  - Securing the Console Line and Disabling the Auxiliary Line 55
  - Securing VTY Access with SSH 56
  - Securing VTY Access with SSH Example 57
  - Securing VTY Access with SSH Using CCP Example 58
  - Securing Configuration and IOS Files 60
  - Restoring Bootset Files 61
- Implementing Role-Based Access Control on Cisco Routers 62
  - Configuring Privilege Levels 62
  - Configuring Privilege Levels Example 62
  - Configuring RBAC via the CLI 62
  - Configuring RBAC via the CLI Example 63
- Configuring Superviews 63
  - Configuring a Superview Example 64
  - Configuring RBAC Using CCP Example 64
- Network Monitoring 67
  - Configuring a Network Protocol Master Clock 67
  - Configuring an NTP Client 67
  - Configuring an NTP Master and Client Example 67
  - Configuring an NTP Client Using CCP Example 68
- Configuring Syslog 69
  - Configuring Syslog Example 71
  - Configuring Syslog Using CCP Example 71
- Configuring SNMP 74
  - Configuring SNMP Using CCP 74

## CHAPTER 7 Securing Management Access with AAA 77

- Authenticating Administrative Access 78
  - Local Authentication 78
  - Server-Based Authentication 78
  - Authentication, Authorization, and Accounting Framework 79
- Local AAA Authentication 79
  - Configuring Local AAA Authentication Example 80
  - Configuring Local AAA Authentication Using CCP Example 81
- Server-Based AAA Authentication 86
  - TACACS+ Versus RADIUS 86
  - Configuring Server-Based AAA Authentication 87
  - Configuring Server-Based AAA Authentication Example 88
  - Configuring Server-Based AAA Authentication Using CCP Example 89
- AAA Authorization 94
  - Configuring AAA Authorization Example 94
  - Configuring AAA Authorization Using CCP 94
- AAA Accounting 98
  - Configuring AAA Accounting Example 98
- Cisco Secure ACS 98
  - Adding a Router as a AAA Client 99
  - Configuring Identity Groups and an Identity Store 99
  - Configuring Access Service to Process Requests 100
  - Creating Identity and Authorization Policies 101

## CHAPTER 8 Securing the Data Plane on Catalyst Switches 103

- Common Threats to the Switching Infrastructure 104
  - Layer 2 Attacks 104
  - Layer 2 Security Guidelines 104
- MAC Address Attacks 105
  - Configuring Port Security 105
  - Fine-Tuning Port Security 106
  - Configuring Optional Port Security Settings 107
  - Configuring Port Security Example 108
- Spanning Tree Protocol Attacks 109
  - STP Enhancement Features 109
  - Configuring STP Enhancement Features 110
  - Configuring STP Enhancements Example 111
- LAN Storm Attacks 112
  - Configuring Storm Control 112
  - Configuring Storm Control Example 113
- VLAN Hopping Attacks 113
  - Mitigating VLAN Attacks 114
  - Mitigating VLAN Attacks Example 114
- Advanced Layer 2 Security Features 115
  - ACLs and Private VLANs 116
  - Cisco Integrated Security Features 116
  - Secure the Switch Management Plane 117

## CHAPTER 9 Securing the Data Plane in IPv6 Environments 119

- Overview of IPv6 119
  - Comparison Between IPv4 and IPv6 119
  - The IPv6 Header 120
  - ICMPv6 121
  - Stateless Autoconfiguration 122
  - IPv4-to-IPv6 Transition Solutions 122
  - IPv6 Routing Solutions 122
- IPv6 Threats 123
  - IPv6 Vulnerabilities 124
- IPv6 Security Strategy 124
  - Configuring Ingress Filtering 124
  - Secure Transition Mechanisms 125
  - Future Security Enhancements 125

## Part III: Threat Control and Containment

### CHAPTER 10 Planning a Threat Control Strategy 127

- Threats 127
  - Trends in Information Security Threats 127
- Threat Control Guidelines 128
  - Threat Control Design Guidelines 128
- Integrated Threat Control Strategy 129
  - Cisco Security Intelligence Operations 130

### CHAPTER 11 Configuring ACLs for Threat Mitigation 131

- Access Control List 131
  - Mitigating Threats Using ACLs 132
  - ACL Design Guidelines 132
  - ACL Operation 132
- Configuring ACLs 134
  - ACL Configuration Guidelines 134
  - Filtering with Numbered Extended ACLs 134
  - Configuring a Numbered Extended ACL Example 135
  - Filtering with Named Extended ACLs 135
  - Configuring a Named Extended ACL Example 136
  - Configuring an Extended ACL Using CCP Example 136
- Enhancing ACL Protection with Object Groups 140
  - Network Object Groups 140
  - Service Object Groups 140
  - Using Object Groups in Extended ACLs 141
  - Configuring Object Groups in ACLs Example 142
  - Configuring Object Groups in ACLs Using CCP Example 144
- ACLs in IPv6 149
  - Mitigating IPv6 Attacks Using ACLs 149
  - IPv6 ACLs Implicit Entries 149
  - Filtering with IPv6 ACLs 149
  - Configuring an IPv6 ACL Example 151

### CHAPTER 12 Configuring Zone-Based Firewalls 153

- Firewall Fundamentals 153
  - Types of Firewalls 154
- Firewall Design 154
- Firewall Policies 154
- Firewall Rule Design Guidelines 155
- Cisco IOS Firewall Evolution 155
- Cisco IOS Zone-Based Policy Firewall 156
- Cisco Common Classification Policy Language 156
- ZFW Design Considerations 156
- Default Policies, Traffic Flows, and Zone Interaction 157
- Configuring an IOS ZFW 157
- Configuring an IOS ZFW Using the CLI Example 160
- Configuring an IOS ZFW Using CCP Example 161
- Configuring NAT Services for ZFWs Using CCP Example 167

### CHAPTER 13 Configuring Cisco IOS IPS 171

- IDS and IPS Fundamentals 171
  - Types of IPS Sensors 172
  - Types of Signatures 172
  - Types of Alarms 172
- Intrusion Prevention Technologies 173
  - IPS Attack Responses 174
  - IPS Anti-Evasion Techniques 175
  - Managing Signatures 175
  - Cisco IOS IPS Signature Files 176
  - Implementing Alarms in Signatures 176
  - IOS IPS Severity Levels 177
  - Event Monitoring and Management 177
  - IPS Recommended Practices 178
- Configuring IOS IPS 178
  - Creating an IOS IPS Rule and Specifying the IPS Signature File Location 179
  - Tuning Signatures per Category 180
  - Configuring IOS IPS Example 183
  - Configuring IOS IPS Using CCP Example 185
  - Signature Tuning Using CCP 193

## Part IV: Secure Connectivity

### CHAPTER 14 VPNs and Cryptography 195

- Virtual Private Networks 195
  - VPN Deployment Modes 196
