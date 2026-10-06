socket so we issue the command “sock_get_once”.
Next, we build our buffer. We start out by using rand_text_alpa to generate random alphabet characters instead of just sending A’s. This is so that the exploit looks a bit more random. We append the EIP value that we got from our initialize function and then use the “pack” function to turn into network byte order. We append 32 NOP instructions through make_nops. We append our encoded payload that Metasploit will generate for us when we send a payload inside msfconsole. It knows based on the size restrictions we placed how big the encoded payload can be so that ensures we don’t generate a buffer that is too large. Finally, we call make_nops again to fill in the rest of our 1024 characters with NOP instructions.

The next step is to send the exploit, so we print out a status message and then send our buffer to the payload to decide what to do next. Metasploit will handle this for us, so all we need to do is to disconnect from the remote system. We print out the status message and disconnect, and then end our exploit function.

# Executing the Exploit

Let’s try it out. We load the Metasploit console by typing msfconsole - q at the command prompt. Once we see the msf > prompt, we are ready to go. Fig. 9.11 shows the sequence of commands we need to use to configure the vuln exploit. We use the module we created by typing use exploit/linux/vuln. This is the path we used to save the module in our home directory. Next, we configure the RHOST variable to set the target we will be exploiting, in this case

127.0.0.1.