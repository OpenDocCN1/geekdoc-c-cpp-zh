and network information. At times, we may want one, two, or all three options. To do this, we will use the built-in option handling in Metasploit. Let's take a look.

# ##

```
# This module requires Metasploit:
h://metasploit.com/download
# Current source: https://github.com/rapid7/metasploit-framework
require 'msf/core'
require 'rex'
class Metasploit3 < Msf::Post
  include Msf::Post::Windows::Registry
  include Msf::Post::Windows::Accounts
  include Msf::Post::Windows::WMIC
  def initialize(info = {})
    super(update_info(info,
      'Name' => 'Gather Basic Information About a System',
      'Description' => 'This module will enumerate users, groups, and network information',
      'License' => MSF_LICENSE,
      'Author' => ['Ryan Linn <sussurro[at]happypacket.net>'],
      'Platform' => ['win'],
      'SessionTypes' => ['meterpreter'])
    )
    register_options(
      [
        Opt.string('INFO', [false, 'Information to gather \U(ser)G(roup)N(network)']
      ], self.class)
  end
```

This looks very similar to the start of our exploit module. We are including a series of Mix-Ins that will allow us to interact with the Registry, Accounts, and WMIC. We include the standard information in the initialize function, but notice here we don't have to set anything about a payload because there is no payload. We also have a block of code to register options. In this case, we have created a string called INFO that someone can set values they want to retrieve. We can put U for user, G for group, or N for network, or any combination of the previous values to retrieve multiple pieces of data in one pass.