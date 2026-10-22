```
puts Time.now                 #=> Thu May 18 23:29:14 CDT 2006
puts 20.minutes.ago           #=> Thu May 18 23:09:14 CDT 2006
puts 20.hours.from_now        #=> Fri May 19 19:29:14 CDT 2006
puts 20.weeks.from_now        #=> Thu Oct 05 23:29:14 CDT 2006
puts 20.months.ago            #=> Sat Sep 25 23:29:16 CDT 2004
puts 20.minutes.until("2006-12-25 12:00:00".to_time)
                             #=> Mon Dec 25 11:40:00 UTC 2006
puts 20.minutes.since("2006-12-25 12:00:00".to_time)
                             #=> Mon Dec 25 12:20:00 UTC 2006
```

How cool is that? And it gets even cooler....

# 16.6  Time and Date Extensions

The Time class gains a number of useful methods, helping you calculate relative times and dates and format time strings. Many of these methods have aliases; see the API documentation for details.

```
now = Time.now
puts now                         #=> Thu May 18 23:36:10 CDT 2006
puts now.to_date                 #=> 2006-05-18
puts now.to_s                    #=> Thu May 18 23:36:10 CDT 2006
puts now.to_s(:short)            #=> 18 May 23:36

puts now.to_s(:long)             #=> May 18, 2006 23:36
puts now.to_s(:db)               #=> 2006-05-18 23:36:10
puts now.to_s(:rfc822)           #=> Thu, 18 May 2006 23:36:10 -0500
puts now.ago(3600)               #=> Thu May 18 22:36:10 CDT 2006
puts now.at_beginning_of_day     #=> Thu May 18 00:00:00 CDT 2006

puts now.at_beginning_of_month  #=> Mon May 01 00:00:00 CDT 2006
puts now.at_beginning_of_week   #=> Mon May 15 00:00:00 CDT 2006
puts now.at_beginning_of_quarter#=> Sat Apr 01 00:00:00 CST 2006
puts now.at_beginning_of_year   #=> Sun Jan 01 00:00:00 CST 2006
puts now.at_midnight             #=> Thu May 18 00:00:00 CDT 2006

puts now.change(:hour => 13)     #=> Thu May 18 13:00:00 CDT 2006
puts now.last_month              #=> Tue Apr 18 23:36:10 CDT 2006
puts now.last_year               #=> Wed May 18 23:36:10 CDT 2005
puts now.midnight                #=> Thu May 18 00:00:00 CDT 2006
puts now.monday                  #=> Mon May 15 00:00:00 CDT 2006

puts now.months_ago(2)           #=> Sat Mar 18 23:36:10 CDT 2006
puts now.months_since(2)         #=> Tue Jul 18 23:36:10 CDT 2006
puts now.next_week               #=> Mon May 22 00:00:00 CDT 2006
puts now.next_year               #=> Fri May 18 23:36:10 CDT 2007
puts now.seconds_since_midnight  #=> 84970.423472

puts now.since(7200)             #=> Fri May 19 01:36:10 CDT 2006
puts now.tomorrow                #=> Fri May 19 23:36:10 CDT 2006
puts now.years_ago(2)            #=> Tue May 18 23:36:10 CDT 2004
puts now.years_since(2)          #=> Sun May 18 23:36:10 CDT 2008
puts now.yesterday               #=> Wed May 17 23:36:10 CDT 2006
```