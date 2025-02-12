Unix groups are traditionally defined in `/etc/group` file.

Try to cat out the `/etc/group` file to see the groups on your unix system.  
Notice: their is a group called by your username (example below is:  `martyi`)

```
martyi@C240071:~$ cat /etc/group
...
...
systemd-resolve:x:991:
uuidd:x:103:
_ssh:x:104:
landscape:x:105:
polkitd:x:990:
admin:x:106:
netdev:x:107:martyi
martyi:x:1000:        <=== martyi group has id 1000
docker:x:1001:martyi  <=== docker group has id 1001 and has a user member `martyi`
                    NOTE:  user/member `martyi` is found in the /etc/passwd file
...
...
```
`

`

To add a new group you can run [groupadd](https://www.redhat.com/en/blog/linux-groups)

or just simply edit the file and add the group with a unique id and users/members.
