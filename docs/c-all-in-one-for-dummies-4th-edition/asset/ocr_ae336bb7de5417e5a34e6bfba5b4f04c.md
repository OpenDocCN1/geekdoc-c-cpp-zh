# # ENSURE THAT YOUR COMPILER IS SUPPORTED

Boost constantly adds new libraries and functionality. To provide these new features, the developers who create Boost have to make some hard decisions. One of the hardest decisions is whether to continue supporting older compilers (and possibly hold Boost development back) or to drop support for some compilers in order to make Boost better.

Boost 1.73.0 is the current version as of this writing, and is the version used for the examples (using a different version may cause some examples to fail). You can view compiler support details at https://www.boost.org/doc/libs/1_73_0/libs/log/doc/html/log/installation.html that includes caveats, such as the use of compiler optimization in some cases. As a result, if you're using this book with an older compiler, the examples in this chapter and Chapter 5 of this minibook may not work. (In fact, they probably won't.) If you plan to use Boost extensively, it pays to subscribe to its RSS feed for additional information.

In addition to the Boost-specific information, please be sure to check for book-specific information on my blog at http://blog.johnmuellerbooks.com/categories/263/c-all-in-one-for-dummies.aspx. I'll provide updates as readers bring issues to my attention. In addition, my blog is the place to look for information regarding the effect of Boost updates on book examples and so on. Please be sure to contact me at John@JohnMuellerBooks.com with your questions and concerns regarding book examples.

# ## Licensing

The Boost license is friendly to individual users, consultants, and organizations. Even if you work in an enterprise environment, you can use Boost for free. The developers behind Boost are concerned enough about legal matters that they continue working on the license so that usage requirements are easy to understand. You can find a copy of the current license at https://www.boost.org/users/license.html.

![](bbox=[0.164, 0.748, 0.239, 0.809])

The Boost license and the GNU General Public License (GPL) differ in some important ways. The most important consideration for organizations is that the Boost license lets you make changes to the libraries without having to share these changes with anyone. You get to keep your source code secret, which is a big plus for organizations that create commercial applications.