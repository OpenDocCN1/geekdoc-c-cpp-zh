This chapter was written by Mike Clark (http://clarkware.com). Mike is an independent consultant, author, and trainer. Most important, he’s a programmer. He helps teams build better software faster using agile practices. With an extensive background in J2EE and test-driven development, he’s currently putting his experience to work on Rails projects.

# Chapter 14

# Task T: Testing

In short order we’ve developed a respectable web-based shopping cart application. Along the way, we got rapid feedback by writing a little code and then punching buttons in a web browser (with our customer by our side) to see whether the application behaved as we expected. This testing strategy works for about the first hour you’re developing a Rails application, but soon thereafter you’ve amassed enough features that manual testing just doesn’t scale. Your fingers grow tired and your mind goes numb every time you have to punch all the buttons, so you don’t test very often, if ever.

Then one day you make a minor change and it breaks a few features, but you don’t realize it until the customer phones you to say she’s no longer happy. If that weren’t bad enough, it takes you hours to figure out exactly what went wrong. You made an innocent change over here, but it broke stuff way over there. By the time you’ve unraveled the mystery, the customer has found herself a new best programmer.

It doesn’t have to be this way. There’s a practical alternative to this madness: write tests!

In this chapter, we’ll write automated tests for the application we all know and love—the Depot application.¹ Ideally, we’d write these tests incrementally to get little confidence boosts along the way. Thus, we’re calling this Task T, because we should be doing testing all the time. You’ll find listings of the code from this chapter starting on page 713.

# 14.1 Tests Baked Right In

With all the fast and loose coding we’ve been doing while building Depot, it would be easy to assume that Rails treats testing as an afterthought. Nothing

1. We’ll be testing the stock, vanilla version of Depot. If you’ve made modifications (perhaps by trying some of the playtime exercises at the ends of the chapters), you might have to make adjustments.