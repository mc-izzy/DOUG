When a script (such as bash, perl, or python) is run in Unix it must have an interpreter.  You can either give the interpreter first on the command line and pass the script to it or you can make the script executable and then put the interpreter on the first line of the file.


## What if you want to run a bash script?
Given the following file `test.sh`
```
#!/usr/bin/bash
echo "Hello World!"
```

And given the following permissions.  The only way to execute the file without changing the permissions is to run bash and pass the test.sh script as an argument.
```
> ls -al test.sh
-r--r--r-- 1 martyi martyi 36 Jan 19 21:19 test.sh

> bash test.sh
Hello World!
```




How to make the above script executable and then just run it?
```
chmod 755 test.sh
./test.sh
Hello World!
```




## What if you want to run a perl script.
Given the following perl script `testing.pl`
```
print "Hello Perl!\n";
```

And given the following permissions.  The only way to execute the perl script file without changing the permissions is to run perl and pass the testing.pl script as an argument.
```
> ls -al testing.pl
-r--r--r-- 1 martyi martyi 36 Jan 19 21:19 testing.pl

> perl testing.pl
Hello Perl!
```

 How to make the above script executable and then just run it?
```
chmod 755 testing.pl
./testing.pl
./testing.pl: line 1: print: command not found
```

Why did we get an error?  Can you explain why?
How can we fix it?

