## How does Linux Umask work?

The _umask_ command works by stripping away permissions as the file is created. On the system, the default _umask_ is currently set to the octal value of 022. Here is what it looks like in the terminal.

```
[root@host umask]# umask
0022
```

To understand with which permissions files and directories are made when _umask_ is set to 022, simply subtract that value from the default permissions Linux sets for files and directories before _umask_ which is 666 for files and 777 for directories.

- New files: 666 – 022 = 644
- New directories: 777 – 022 = 755

### Example: use default umask to create a file and directory
```
> touch test0.txt
> ls -al 
-rw-r--r-- 1 martyi martyi    0 Feb 12 08:37 test0.txt

> mkdir dir0
> ls -al
drwxr-xr-x 2 martyi martyi 4096 Feb 12 08:38 dir0
-rw-r--r-- 1 martyi martyi    0 Feb 12 08:37 test0.txt
```


### Example:  Change umask to 0066
- New files: 666 – 066 = 600
- New directories: 777 – 066 = 711
```
> umask 0066
> touch test1.txt

> ls -al
drwxr-xr-x 2 martyi martyi 4096 Feb 12 08:38 dir0
-rw-r--r-- 1 martyi martyi    0 Feb 12 08:37 test0.txt
-rw------- 1 martyi martyi    0 Feb 12 08:39 test1.txt

> mkdir dir1
> ls -al
drwxr-xr-x 2 martyi martyi 4096 Feb 12 08:38 dir0
drwx--x--x 2 martyi martyi 4096 Feb 12 08:39 dir1
-rw-r--r-- 1 martyi martyi    0 Feb 12 08:37 test0.txt
-rw------- 1 martyi martyi    0 Feb 12 08:39 test1.txt
```

### Now change umask back to 0022
- New files: 666 – 022 = 644
- New directories: 777 – 022 = 755
```
> umask 0022
> touch test2.txt

> mkdir dir2
> ls -al
drwxr-xr-x 2 martyi martyi 4096 Feb 12 08:38 dir0
drwx--x--x 2 martyi martyi 4096 Feb 12 08:39 dir1
drwxr-xr-x 2 martyi martyi 4096 Feb 12 08:41 dir2
-rw-r--r-- 1 martyi martyi    0 Feb 12 08:37 test0.txt
-rw------- 1 martyi martyi    0 Feb 12 08:39 test1.txt
-rw-r--r-- 1 martyi martyi    0 Feb 12 08:40 test2.txt
```