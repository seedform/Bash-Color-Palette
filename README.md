# color256
A bash script to test and get escape sequences for 256 terminal colors.

```
$ color256
Usage: color256 [-a] [-b num] [-f num]
    -a  display all colors
    -b  display the background color escape sequence for num
    -f  display the foreground color escape sequence for num
    num should be a value from 0 to 255.

$ color256 -f 200
\e[38;5;200m
```

![](https://raw.githubusercontent.com/seedform/color256/master/20160221144140.png)

Tested on Bash 4.3 on Arch Linux.
