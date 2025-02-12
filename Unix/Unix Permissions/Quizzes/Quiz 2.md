![[Unix Permissions Drawing.png]]

![[Controlling Unix Permissions]]


## Create a directory that has the SGID bit set `on` so that files created under it  inherit the directory permissions

#### Example #1
```
> mkdir inherit_grp_of_parent_dir
> chmod 2775 inherit_permissions
> ls -al 
> drwxrwsr-x 2 martyi martyi 4096 Feb 12 09:55 inherit_permissions

> cd inherit_permissions
> touch inherit.txt
> ls -al 
> 
```