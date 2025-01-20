
![[Controlling Unix Permissions]]


## Changing Unix **File** Permissions Examples
### The way to control permission is to use the `chmod` command

#### Example #1
```
> cd /home/martyi
> echo 'This is a test of the emergency broadcast system...' > testing.txt
> chmod 644 testing.txt

> ls -al
-rw-r--r-- 1 martyi martyi 52 Jan 19 20:24 testing.txt
```   

##### Quiz #1
Who can see the contents of this file and why?


#### Example #2
```
> cd ~
> echo 'This is a test of the emergency broadcast system...' > testing2.txt
> chmod 600 testing2.txt

> ls -al
-rw------- 1 martyi martyi 52 Jan 19 20:24 testing.txt
```

##### Quiz #2
Who can edit the contents of this file and why?   Who cannot edit this file?



#### Example #3
```
cd /home/martyi

```

