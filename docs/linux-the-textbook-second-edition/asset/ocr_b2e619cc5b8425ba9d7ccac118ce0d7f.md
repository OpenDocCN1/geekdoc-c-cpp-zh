# 8

# File Sharing

# OBJECTIVES

+   - To explain different ways of sharing files
+   - To discuss the Linux schemes and commands for implementing file sharing
+   - To describe Linux hard and soft (symbolic) links in detail and discuss their advantages and disadvantages
+   - To cover the following commands and primitives:
+     `*, ~, df, ln, ln -f, ln -s, ls -i, ls -l`

# 8.1 Introduction

When a group of people works together on a project, they need to share information. If the information to be shared is on a computer system, group members have to share files and directories. For example, authors collaborating on a book or software engineers working on a software project need to share files and directories related to their project. In this chapter, we discuss several ways of implementing file sharing in a computer system. The discussion of file sharing in this chapter focuses on how a file can be accessed from various directories by various users in a Linux system. Under the topic of version control in Chapter 14 and in Chapter W25, Section 5.7 at the book website, we address how members of a team can work on one or more files simultaneously without losing their work.

Several methods can be used to allow a group of users to share files and directories. In this chapter, we describe duplicate shared files, common logins for members of a team, setting appropriate access permissions on shared files, common groups for members in a team, and sharing via links. All these methods can be used to allow a team of users to share files and directories in a Linux system. Although we describe each of these techniques, the chapter is dedicated primarily to a discussion of sharing via links in a Linux-based computer system.

# 8.2 Duplicate Shared Files

The simplest approach to files is to make copies of these files and give them to all team members. The members can put these copies anywhere in their own accounts (directory structures) and manipulate them in any way they desire. This scheme works well if members of the team are to work on the shared file(s) sequentially, but it has obvious problems if team members are to work on these files simultaneously. In the former case, team members work on one copy of the shared files one by one and complete the task at hand. In the latter case, because the members modify their own copies, the copies become inconsistent and no single copy of the shared files reflects the work done by all the team members. This outcome defeats the purpose of sharing.

# 8.3 Common Logins for Team Members

In this scheme, the system administrator creates a new user group comprising the members of a team and creates for them a new account to which they all have access; that is, they all know the login name and