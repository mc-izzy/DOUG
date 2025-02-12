![[Unix Permissions Drawing.png]]


![[Controlling Unix Permissions]]



## Bring up the `wsl` window on your laptop.  
* create the following directory structure
```
> mkdir DOUG
> cd DOUG
> mkdir unix_permissions
> cd unix_permissions
```


## Changing Unix **File** Permissions Examples
### The way to control permission is to use the `chmod` command

#### Example #1
```
> cd /home/martyi
> echo 'This is a test of the emergency broadcast system...' > testing.txt
> chmod 644 testing.txt

> ls -al
-rw-r--r-- 1 martyi web 52 Jan 19 20:24 testing.txt
```   

##### Quiz
Who can see the contents of this file and why?


#### Example #2
```
> cd ~
> echo 'This is a test of the emergency broadcast system...' > testing2.txt
> chmod 600 testing2.txt

> ls -al
-rw------- 1 martyi web 52 Jan 19 20:24 testing.txt
```

##### Quiz
Who can edit the contents of this file and why?   Who cannot edit this file?




## Create a file and change it's permissions so that:
*  User:    has `read` & `write` & `execute`
* Group:  has `read` only
* World:  has `read` only
### Quiz
```
> touch my_executable.sh
> chmod ??? my_executable.sh
```


## Now change the permissions so that:
*  User:    has `read` & `write`
* Group:  has `read` & `write` 
* World:  has `read` & `write`
### Quiz
```
> chmod ??? my_executable.sh
```
