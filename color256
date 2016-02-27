#!/usr/bin/env bash

#
# (c) 2016 Shudmanul Chowdhury
#
# A simple script to test and get escape sequences for 256 terminal colors.
#

NAME="${0##*/}"
UNDER="\e[4m"
RESET="\e[0m"
TCOLS=$(tput cols)

# prints foreground escape sequence
fgc() {
    echo "\e[38;5;${1}m"
}

# prints background escape sequence
bgc() {
    echo "\e[48;5;${1}m"
}

usage() {
    while IFS= read -r line; do
        echo -e "$line"
    done << EOF
Usage: $NAME [-a] [-b num] [-f num]
    -a  display all colors
    -b  display the background color escape sequence for ${UNDER}num${RESET}
    -f  display the foreground color escape sequence for ${UNDER}num${RESET}
    ${UNDER}num${RESET} should be a value from 0 to 255.
EOF
    exit 1
}

# displays all 256 colors
disp() {
    local c # color code

    # print basic colors
    echo "Basic (0 to 15):"
    for c in {0..15}; do
        # set the background color to its respective color code
        echo -en "$(bgc $c)   $RESET"
    done
    printf "\n\n"

    # print greyscale
    echo "Greyscale (232 to 255):"
    for c in {232..255}; do
        # set the background color to its respective color code
        echo -en "$(bgc $c)  $RESET"
    done
    printf "\n\n"

    # show a chart of six 6x6 color palettes
    echo "6x6x6 Cubic Palette (16 to 231): "
    local colc=0                # column counter
    local sixs=$(($TCOLS / 30)) # number of 6x6 palettes across screen
    local cols=$(($sixs * 6))   # number of color columns (5 characters wide)
    c=16                        # starting color code
 
    while [[ $c -lt 232 ]]; do  # 16 to 231

        # set the background color to its respective color code
        printf "$(bgc $c) %03d $RESET" "$c"

        # increment the color code and the 
        ((c++))
        ((colc++))

        # enter a new line if the terminal width has been reached
        if [[ $colc -eq $cols ]]; then

            # go back to the first set of 6x6 colors on this line if any left
            if [[ $((($c - 16) % 36)) -ne 0 ]]; then
                c=$(($c - ($sixs - 1) * 36))
            fi

            colc=0  # go back to the first column
            echo    # new line

        # go to the next set of 6x6 colors
        elif [[ $(($colc % 6)) -eq 0 ]] && [[ $(($c + 30)) -lt 232 ]]; then
            ((c+=30))
        fi        
    done
    echo -e $RESET
}

# process only one option
if getopts ab:f: OPT; then
    case "$OPT" in
    a)  # display all colors
        disp
        ;;
    b|f)# display escape sequence
        if [[ $OPTARG =~ ^[0-9]+$ && $OPTARG -ge 0 ]]; then
            [[ $OPT == "b" ]] && bgc $OPTARG
            [[ $OPT == "f" ]] && fgc $OPTARG
            exit 0
        else
            usage
        fi
        ;;
    esac
else
    usage
fi
