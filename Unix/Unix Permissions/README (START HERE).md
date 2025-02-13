# Unix Permissions
Unix permissions are ==a system that controls who can access a file or directory on a Unix-based system==, allowing specific users (the file **`owner`**, **`group`** members, and **`everyone else`**) to perform actions like reading, writing, or executing based on assigned permissions, which are typically categorized as **"read,"** **"write,"** and **"execute"** for each user group. 

# Key points about Unix permissions:

## Three access levels
* Each file/directory has three access levels
	* Owner:   the file **`owner`** - owners/users are defined in [/etc/passwd](Unix%20Users.md) 
    * Group:   the **`group`** the file belongs to, groups are defined in [/etc/group](Unix%20groups.md)
    * Other:  **`"others"`** (everyone else). 
## Three permissions for `files`
* Within each user group, you can set 
    * ***"read,"**   -- View the file contents
    * **"write,"**   -- Modify the file
    * **"execute"** -- Allow to run as a program
    
## Three permissions as they related to `Directory access`
* When applied to directories:
	 "read"       --  lets you list files within the directory, 
     "write"      -- allows you to create, delete, or rename files
     "execute"  -- grants access to enter the directory

## Why are Unix permissions considered better than windows permissions**

Unix permissions are often considered better than Windows permissions because ==they offer a more granular and robust system for controlling file access==, with a clear hierarchy of user, group, and "other" permissions, allowing for precise control over who can read, write, and execute files, while Windows permissions can be more complex and often rely on broader "Everyone" group access by default, potentially leading to less secure configurations.


 
## Nice summary picture of Unix Permissions:
 ![[Unix Permissions Drawing.png]]


 ![[Controlling Unix Permissions]]

# Now try  [[Quiz 1]]



## Umask Explained
![[umask explained]]

## --> Now you try the example above



# Special permissions explained (SUID, GUID, Sticky bit)

![[Special permissions explained]]


## Now try [[Quiz 2]]

test





