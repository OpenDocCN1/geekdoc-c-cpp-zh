```
$body = $response->content;
$parsed = HTML::Parse::parse_html($body);
for (@{$parsed->extract_links(qw(a))}) {
    ($link) = @$link;
    if ($link ~ /m/url/) {
        print $link . "\n";
    }
}
```

Let's look at what we did here. At the top, we have our shebang to point out, as well as a few lines to set up our module usage for the script. Here we will be using the LWP::UserAgent and HTML::Parse modules to do the heavy lifting for us. We also take in a couple of arguments: The name of the site goes into $site and the file type we are looking for goes into $filetype.

Next, we put together our search URL for Google. The string in $searchurl is a simple Google search, with the values in $site and $filetype plugged in, in the appropriate places. We then set up our user agent and its details, $userdata, as well as setting the agent string to Mozilla/4.0 (compatible; MSIE 5.0; Windows 95). The agent is an option here, but if we don't set it, Google will not talk to us, as we think we are a script and not a real browser, so we really do need it here.

# Warning

The Google search used in this script is not the approved way to talk to Google with automation. If we're not careful and we abuse this type of connection, Google will get mad and ban our IP address. Google has happily documented the proper way for us, and we should really be using that. This is a bit out of scope for what we're doing here, but the documentation will get us there for constructing our queries in the approved manner.

After this, we request our page using HTTP::Request. We instantiate a new object, with $request as the handle, use that to request our page, place the response into $response, and pull out the actual content of the page into $body.