not a string object such as "http://www.apple.com", but it's easy to create one from a string object using the URLWithString: method.
Program 16.9 shows how the html contents from a web address can be read into a program.

# Program 16.9

```
// Read the contents of a file stored at a URL

#import <Foundation/Foundation.h>

int main(int argc, char * argv[]) {
    NSAutleasePool *pool = [NSAutleasePool alloc] init];
    myURL = [NSURL URLWithString:"http://classroomM.com"];

    NSString *myHomePage = [NSString stringContentsOfURL:myURL encoding:NSASCIIStringEncoding error:NULL];

    NSLog("%@@", myHomePage);

    [pool drain];
    return 0;
}
```

# Program 16.9 Output

```
<!DOCTYPE html PUBLIC-//W3C//DTD HTML 1.0 Transitional//EN"
n"http://www.w3.org/TR/xhtml/xhtml1-transitional.dtd">
<html xmlns="http://www.w3.org/1999/xhtml"><head>
<meta http-equiv="Content-Type" content="text/html; charset=iso-8859-1" />
<meta http-equiv="Content-Style" content="text/css" />
<meta name="google-site-verification"
content="75Jblby6mQtiHzHdXWphlnBnC3rUC0COLj8glzjy98" />
<title>iPhone Online Course and iPhone Programming Training - Home</title>
```

You can see how easy it is to get data from the Internet. And if you use a dictionary stored in a property list with an address, you can read that in as well, using the dictionaryContentsOfURL: method. Or if it's array stored as a property list, you can use the arrayContentsOfURL: method instead. You may also want to look into the dataWithContentsOfURL: method.

# The NSBundle Class

When you create an application, the system stores all the data associated with that application—which includes resources as images, localized strings, icons, and so on—into a package known as an application bundle. In order to access those resources from your application, you must become familiar with the NSBundle class.

It's easy to add a resource like an image or a file to your application: simply drag the file into the left pane in Xcode. When prompted, you'll usually want to copy the resource into your project folder, so that your project is self-contained.