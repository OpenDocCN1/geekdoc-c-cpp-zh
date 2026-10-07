which your programs are stored (or just simply the current directory) to the shell's PATH
variable. Let's take the first approach here:

```
$ ./progl Execute progl
2008-06-08 18:48:44.210 progl[7985:10b] Programming is fun!
$
```

You should note that writing and debugging Objective-C programs from the terminal
is a valid approach. However, it's not a good long-term strategy. If you want to build Mac
OS X or iOS applications, it's just to use the executable file that needs to be
"packaged" into an application bundle. It's not easy to do that from the Terminal applica-
tion, and it's one of Xcode's specialties. Therefore, I suggest you start to use
Xcode to develop your programs. There is a learning curve to do, but the effort will
be worth it in the end.

# Explanation of Your First Program

Now that you are familiar with the steps involved in compiling and running Objective-C
programs, let's take a closer look at this first program. Here it is in again:

```
// main.m
// progl
```

> // Created by Steve Kochan on 1/30/11.
// Copyright 2011 ClassroomM, Inc.. All rights reserved.

```
#import <Foundation/Foundation.h>

int main (int argc, const char *argv[]) {
   NSAutleasePool *pool = [NSAutleasePool alloc init];

   NSLog("@Programming is fun!");

   [pool drain];
   return 0;
}
```

In Objective-C, lowercase and uppercase letters are distinct. Also, Objective-C doesn't
care on the line where you begin—you can begin your statement at any position on
tline.You can use this to your advantage in developing programs that are easier to read.

The first seven lines of the program introduce the concept of the comment. A comment
statement is used in a program to document a program and enhance its readability. Com-\ments tell the reader of the program—whether it's the programmer or someone else