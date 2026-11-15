```
} if((j+1)%TEN == 0) fout << endl;
//out << endl;
}
fout.close();
}
void writeHeader(ofstream& out, int h, int w, string comment)
{
out << magicNumber << endl;
////MagicNumber defined in header file
out << "**comment"<<endl;
out << h << " " << w << endl;
out << maxPixelVal << endl;
////maxPixelVal defined in header file
}
```

# Xcode

Create a new project in Xcode by selecting New-> Project... from the File menu at the top left of the main Xcode window. For this solution, we will select Application under OS X and Command Line Tool as illustrated in the new project window below.

![](bbox=[0.24, 0.49, 0.87, 0.79])

New Project Window

Select Next to create and save your new project. Add the files Pixel.cpp and Pixel.h to your project and insert the code for the Pixel class declaration and definition as defined in Section 10.1. Recall that you can add a new source file to your project by selecting New -> File... from the Xcode File menu, then select Source and C++File as shown in the new file window below.