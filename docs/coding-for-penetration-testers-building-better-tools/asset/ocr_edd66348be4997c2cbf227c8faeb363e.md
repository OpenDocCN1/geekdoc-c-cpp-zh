# CHAPTER 10

# Postextploitation scripting

# Abstract

Once the shells come back, we have a bit more work to do. This chapter discusses what happens after we've gotten in. Working from information gathering under Windows, and moving towards maintaining access through creating users using the Windows command line, this chapter looks at how to query and manipulate Windows systems from the command line. We've gotten the hang of it, this chapter works to convert that work into a Meterpreter script using Ruby where we can easily run these commands through Metasploit

After exploiting a Web application, we don't want the database to feel out, so this chapter ends with manipulating SQL injection vulnerabilities to gain access to applications, dump data, and even get a shell. While looking at capabilities of MySQL and Microsoft SQL Server, this chapter helps develop postextploitation abilities that will start a basic Web application tester on the road to becoming an advanced one.

# Keywords

Postextploitation; Windows; Meterpreter; Ruby; SQL injection; shell; MySQL; SQL Server

# INFORMATION IN THIS CHAPTER

+   * Why Postextploitation Is Important?
* Windows Shell Commands
* Gathering Network Information
* Scripting Metasploit Meterpreter
* Database Postextploitation

# Introduction