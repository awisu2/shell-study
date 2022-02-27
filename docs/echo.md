# echo study

**documents**

- [echo Man Page \- Linux \- SS64\.com](https://ss64.com/bash/echo.html)

**NOTE**

- with multi line: `echo "$v"`
- color: `\x1b[31m` is change to red. write after

## sample

```bash
# multiline
v=$(cat - << EOC
1
2
EOC
)

echo $v
# 1 2
echo "$v"
# 1
# 2
```

## color

- When the code is interpreted in echo, the string settings are changed.
  - This will continue until the echo ends or another setting is made
- code
  - basic format: `\x1b[{setting}m`
    - thic code has escapable string `\x1b`. so when run echo need `-e` option
  - multi setting: `\x1b[{setting};{setting};{setting}m`
  - set reset: `\x1b[m`
    - setting: has two number `01` = target value. this mean text type(=0) is bold(=1)
    - target: 0: type, 3: text, 4: background
    - value(type): 1: bold, 2: light color, 3: italics, 4: underline, 5: blink, 6: reverse
    - value(color): 0: black, 1: red, 2: green, 3: yellow, 4: blue, 5: purple, 6: aqua, 7: white
- more
  - `\x1b` is escape sequense
    - this is hexadecimal and octalized as `\033`
  - [ANSI escape code \- Wikipedia](https://en.wikipedia.org/wiki/ANSI_escape_code)

```bash
EC_BOLD="01"
EC_LIGHTCOLOR="02"
EC_ITALICS="03"
EC_UNDERLINE="04"
EC_BLINK="05"
EC_REVERSE="06"

EC_TX_BLACK="30"
EC_TX_RED="31"
EC_TX_GREEN="32"
EC_TX_YELLOW="33"
EC_TX_BLUE="34"
EC_TX_PURPLE="35"
EC_TX_AQUA="36"
EC_TX_WHITE="37"

EC_BG_BLACK="40"
EC_BG_RED="41"
EC_BG_GREEN="42"
EC_BG_YELLOW="43"
EC_BG_BLUE="44"
EC_BG_PURPLE="45"
EC_BG_AQUA="46"
EC_BG_WHITE="47"

# direct
COL_RED="\x1b[31m"
COL_BOLD_YELLOW_BG_RED="\x1b[01;33;41m"
COL_RESET="\x1b[m"
echo -e "${COL_RED} hello ${COL_RESET}"
echo -e "${COL_BOLD_YELLOW_BG_RED} hello ${COL_RESET}"

# with argument and withoud -e option
COL_START=$(echo -e "\033") # pre escape
COL_RESET="${COL_START}[m"

# with argument
echo "${COL_START}[${EC_BOLD};${EC_TX_YELLOW};${EC_BG_RED}m hello ${COL_RESET}"

# preset argument
COL_RED="${COL_START}[${EC_TX_RED}m"
COL_BOLD_YELLOW_BG_RED="${COL_START}[${EC_BOLD};${EC_TX_YELLOW};${EC_BG_RED}m"
echo "${COL_RED} hello ${COL_RESET}"
echo "${COL_BOLD_YELLOW_BG_RED} hello ${COL_RESET}"

# function
echo_red() {
    echo "${COL_RED}${1}${COL_RESET}"
}
echo_red "hello"
echo "$(echo_red ""hello"") world"
```
