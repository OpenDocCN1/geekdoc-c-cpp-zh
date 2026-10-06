carry out doesn't call for great complexity, the full set of features is still there if we need to access it.

Let's revisit the code we wrote earlier in the chapter, to pull URLs from Google, but this time we will use WWW::Mechanize instead of LWP::UserAgent:

```
#!/usr/bin/perl
use WWW::Mechanize;
$site = @ARGV[0];
$filetype = @ARGV[1];
$searchurl ="http://www.google.com/search?hl=en&site=$3A$filetype%3A$filetype";n$mech = WWW::Mechanize->new();
$mech->agent_alias('Windows Mozilla');
$mech->get($searchurl);
@links = $mech->find_all_links(url_regex qr/\w+/);
for $link ($links) {
  $url = split //, $link->abs;
  @urlbits = split //, $urlbits[1], 4;
  @moreurlbits = split //, $moreurlbits[3], 2;
  $url = $yemoreurlbits[0];
  if ((length($url) < 1) {next;}
  $filename = s/.*\/([^\/]*)$/$1;
  print "downloading $url to $filename\n";
  $mech->get($url, ':content_file' => $filename);
}
```

We can see here that this code is generally similar to the earlier code module. This is because WWW::Mechanize is largely an extension of the functionality in LWP::UserAgent, and some large portion of it functions very similarly.

# Tip

WWW::Mechanize, developed by Andy Lester [3], is such a commonly used tool that has been implemented in other languages as well, including Python and Ruby. These implementations can be found at http://wwwsearch.sourceforge.net/mechanize/ and http://mechanize.rubyforge.org/, respectively. Thanks for such a great tool, Andy!