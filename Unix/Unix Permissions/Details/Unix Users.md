Unix users are traditionally defined in `/etc/passwd` file.

Try to cat out the `/etc/passwd` file to see the users on your unix system.  
Notice: their is a user called by your username (example below is:  `martyi`)

```
martyi@C240071:~$ cat /etc/passwd
...
...
uuidd:x:103:103::/run/uuidd:/usr/sbin/nologin
landscape:x:104:105::/var/lib/landscape:/usr/sbin/nologin
polkitd:x:990:990:User for polkitd:/:/usr/sbin/nologin
martyi:x:1000:1000:,,,:/home/martyi:/bin/bash       <==== user martyi id of 1000
...                                                       also has grp of 1000
...                                                      home dir is /home/martyi
...                                                     default shell is /bin/bash
...
```


To add a new group you can run [useradd](https://manpages.ubuntu.com/manpages/xenial/man8/useradd.8.html)

or just simply edit the passwd file and add a user with a unique id, group, home dir & shell
