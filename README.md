# color256
A bash script to test and get escape sequences for 256 terminal colors.

![](https://raw.githubusercontent.com/seedform/color256/master/20160221144140.png)

```
$ git clone https://github.com/seedform/color256.git
Cloning into 'color256'...
remote: Counting objects: 15, done.
remote: Compressing objects: 100% (13/13), done.
remote: Total 15 (delta 2), reused 0 (delta 0), pack-reused 0
Unpacking objects: 100% (15/15), done.
Checking connectivity... done.
$ cd color256
$ chmod 755 color256    # remember to set read and execute permissions
$ ./color256
Usage: color256 [-a] [-b num] [-f num]
    -a  display all colors
    -b  display the background color escape sequence for num
    -f  display the foreground color escape sequence for num
    num should be a value from 0 to 255.
$ ./color256 -f 200
\e[38;5;200m
```

Tested on Bash 4.3 on Arch Linux
