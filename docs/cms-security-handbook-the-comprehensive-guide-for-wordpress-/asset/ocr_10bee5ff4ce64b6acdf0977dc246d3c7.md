When run on your server, this tool will test for a number of issues that could affect your security. Figure 5-11 shows an example of one such warning.

![](bbox=[0.099, 0.128, 0.619, 0.321])

**Figure 5-11:** Warning produced by PhpSecInfo tool

This warning appears in red. The various warnings and errors are color-coded. This particular error is telling you that the `force_redirect` directive is disabled. Note the “More information” link on the lower right, which provides you with a detailed explanation of this warning.

At the bottom of the report is the Test Results Summary, as shown in Figure 5-12. It states that 18 tests were run and 10 notices, meaning they need attention. It produced 2 items marked as severe.

![](bbox=[0.099, 0.529, 0.619, 0.654])

**Figure 5-12:** Test Results Summary

You should run this tool regardless of how long your server has been in production. You might find that you have a number of holes. Be sure to run it after any upgrade, or after any incidents that occur.

# php.ini

When you’re using suPHP, you can find a file in the root of most websites called `php.ini`. This file allows you to issue commands to the PHP Interpreter. As was previously stated, you can use this file in place of the `/etc/php.ini` file. Check with your host to ensure the server is running suPHP.

Using WinSCP, locate the `/etc/php.ini` file. If this file does not exist in this directory, it can and may exist in your `public_html` website directory.