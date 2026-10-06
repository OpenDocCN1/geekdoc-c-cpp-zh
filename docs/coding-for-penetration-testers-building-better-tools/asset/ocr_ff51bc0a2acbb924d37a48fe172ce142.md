Next, we create a new instance of the Hypertext Transfer Protocol (HTTP) object using a Ruby technique referred to as a block. The indentation defines the beginning and end of the block. We don't have to use a loop here, but by using this block, we assign our value to the http variable. When our block is over, the Net::HTTP class will close the socket and take care of our cleanup. Our http variable holds the HTTP object which allows us to issue HTTP commands to the Web server. We use the head method to send an HTTP Head request on the Web server as the context. This returns information including the date, the type of Web server, request parameters, and frequently, the last-modified header which indicates when the page was changed. The two pieces of data we are trying to extract from the server are the software being used and the last modified date which we will return as an array.

Finally, we close our loop, allowing the HTTP object to clean up for us. If, for some reason, our request fails, we add a fallback to return an array with nil values. This ensures consistent return information from our function. Let's make our function parse options passed from the command line, and use those variables to call our function.

```
if ARGV.size <= 0 || ARGV.size > 2
print "Usage: ##{$0} Host [Port]\nexit
end
server, modified = getHeader(ARGV[0], ARGV[1])
print "Server ##{ARGV[0]##{ARGV[1]} || 80)(#{server))" last
modified #{(modified)}"
```

# Tip

Notice the difference in the handling of ARGV. In many languages, the first array element in ARGV is the program name itself. In Ruby, the first element of ARGV is the first option. To reference the program name itself, we use $0.

If we have an invalid number of ARGV arguments, we present an error message and exit. The notation we are using in our error string