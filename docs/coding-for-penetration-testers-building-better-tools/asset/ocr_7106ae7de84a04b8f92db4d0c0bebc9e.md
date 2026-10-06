we can better use Perl in order to interact with Web pages, and we will be working with a Perl module called WWW::Mechanize that will allow us a bit more freedom and utility when we work with such targets.

# Web Automation With Perl

In the “Automating Google Discovery” section, we briefly looked at what we could do with Perl in order to talk to a website. When we look at any given task in Perl, or any of the other modern scripting languages, for that matter, there are a number of ways we can approach any given task. The particular module we looked at in the “Automating Google Discovery” section, LWP::UserAgent works admirably for the simple task we put together, but it is only one way to approach what we need to do. In this section, we will take a look at a couple of the alternatives we have for getting similar jobs done.

# Pulling Information From Websites

Let’s look at a very quick and easy method to pull a page from a website. Earlier we used LWP::UserAgent to carry out a similar task, but we can simplify things a bit more by using a similar module, called LWP::Simple. We can even do this from a single command line: perl -MLWP::Simple -e "getprint 'http://www.cnn.com'"

This should get us a result like that shown in Fig. 8.2.