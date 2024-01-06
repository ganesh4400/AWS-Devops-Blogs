---
title: "Day 6 : File Permissions and Access Control Lists 🚀"
datePublished: Tue Oct 31 2023 09:44:24 GMT+0000 (Coordinated Universal Time)
cuid: cloe56tm0000c08mh2pflfw8v
slug: day-6-file-permissions-and-access-control-lists
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1698745045215/6326aa96-d913-4c17-a0a8-8c969206d993.png
tags: linux, devops, shellscripting-devops

---

Welcome to Day 6 of your DevOps journey! Today, we're diving deep into the world of Linux file permissions and access control. Understanding and managing file permissions is fundamental in Linux, and it plays a vital role in securing your system. Let's explore the concepts and tasks for the day.

**Task 1: Explore File Permissions 🕵️‍♂️**

Let's start with a simple task. Create a file and examine its permissions using the "ls -ltr" command. Note how the permissions are displayed.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1698744089676/b70afddb-936b-4903-8db2-6a719f618b11.png align="center")

You'll see a string like "rw-r--r--" which represents permissions for owner, group and others.

**Task 2: Write an Article on File Permissions ✍️**

File permissions in a Linux system are like the gatekeepers of your digital world. They determine who can read, write, and execute files and directories, and they play a crucial role in system security. Whether you're a seasoned sysadmin or just starting your DevOps journey, understanding file permissions is essential. In this article, we'll dive deep into Linux file permissions, covering the concepts, practical usage, and common commands to master this critical aspect of system administration.

## **Understanding File Permissions 🔑**

In Linux, file permissions are divided into three categories, each with its own set of permissions:

1. **Owner**: This is the user who owns the file. The owner has the most control and can change permissions, delete, or modify the file.
    
    Use "chown" to change ownership permissions.
    
2. **Group**: Files often belong to a group, and members of this group have group-level permissions. This is useful when multiple users need access to certain files without giving everyone access.
    
    Use "chgrp" to change group permissions.
    
3. **Others**: Any other user who is not the owner or part of the group falls into this category.
    
    Use "chmod" to change other users' permissions.
    
    ### **Permission Types**
    
    For each of these three categories, there are three types of permissions:
    
    1. **Read (r)**: The ability to view the contents of a file or list the contents of a directory.
        
    2. **Write (w)**: The ability to modify or delete the file, or create new files in a directory.
        
    3. **Execute (x)**: The ability to execute a file as a program or access files and directories.
        
    
    ### **Octal Notation**
    
    File permissions are represented using a combination of letters (r, w, x) and numbers in octal notation (0-7). Each permission type is assigned a numerical value:
    
    * **Read (r)**: 4
        
    * **Write (w)**: 2
        
    * **Execute (x)**: 1
        
    
    These numbers are then added together to represent the permission setting for a file or directory. For example, if you want to give read and execute permissions (4 + 1 = 5), you set it as 5.
    
    ### **Practical Usage**
    
    Let's put this theory into practice. Say you have a file, `my_`[`script.sh`](http://script.sh), and you want to give read and execute permissions to the owner, read-only permissions to the group, and no permissions to others. You can do this using the `chmod` command:
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1698744257624/76019d38-d153-4b80-9d0a-ff92fc957ebf.png align="center")
    
    * The first digit (5) is for the owner.
        
    * The second digit (4) is for the group.
        
    * The third digit (0) is for others.
        
    
    This means that the owner has read and execute permissions (5), the group has read-only permissions (4), and others have no permissions (0).
    
    ### **Changing Ownership**
    
    The `chown` and `chgrp` commands are used to change the ownership and group ownership of a file, respectively.
    
    For example, to change the ownership of a file to a user named "dem," you can use:
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1698744361448/7405e406-fd6d-4cbe-a6aa-c4c8a230510b.png align="center")
    
    ### **Default Permissions**
    
    Default permissions are used to define what permissions new files and directories will have when they are created. They can be set using the `umask` command.
    
    ### **Conclusion**
    
    Understanding Linux file permissions is a fundamental skill for system administrators, DevOps engineers, and anyone working with Linux systems. It's about maintaining security, ensuring data integrity, and granting the right level of access to users and groups. By mastering file permissions, you take a significant step toward becoming a proficient Linux administrator. Keep learning and experimenting, and you'll be well on your way to success in the world of DevOps.
    

# **Task 3: Explore Access Control Lists (ACL) 📜**

Access Control Lists (ACLs) provide even more granular control over file permissions. They allow you to specify permissions for specific users or groups beyond the owner, group, and others. To get started, read about ACLs and try out the commands "getfacl" and "setfacl" to manage ACLs for files and directories.

By the end of today's tasks, you'll have a deeper understanding of file permissions in Linux and the power of ACLs. Your knowledge and practical experience in managing file access will be invaluable in your DevOps journey.

Stay curious keep exploring, and remember to document your findings and experiences. Enjoy Day 6! 🚀

#DevOps #Linux #FilePermissions #ACL #AccessControl #SysAdmin #LearningAndGrowing