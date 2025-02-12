![[Unix Permissions Drawing.png]]

![[Controlling Unix Permissions]]


## Create a directory that has the SGID bit set `on` so that files created under it  inherit the unix group

# Example #1
```
> mkdir inherit_group
> chmod 2775 inherit_group
> chgrp users inherit_group
> ls -al 
> drwxrwsr-x 2 martyi users 4096 Feb 12 09:55 inherit_permissions

> cd inherit_group
> touch inherit.txt
> ls -al 
-rw-r--r-- 1 martyi users     0 Feb 12 15:39 inherit.txt
```

## Notice:  
* Once you created the file it now has inherited the group from the parent directory (`users`). because the SGID bit is set on.

## Question: 
* Why didn't it inherit the permissions of `rw-rw-r--`
* **Answer:**   Because that is controlled by the `umask` still;)
	* See: [[umask explained]]

## Why is this useful?
* This is useful if multiple people/developers want to work on files under a single directory





