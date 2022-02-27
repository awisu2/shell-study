# here document

- [Here Documents](https://tldp.org/LDP/abs/html/here-docs.html)

**NOTE**

- The charactor EOC is the sample specifies the start and end of the here document.
  - Any character will do. EOC is a coined word, meaning end of code.
- Document start from second line.
- if don't want expand variables, to change EOC > 'EOC'.

## sample

```bash
strB="b"
cat << EOC
a
$strB
EOC
# a
# b
```

**not expand variables**

```bash
strB="b"
cat << 'EOC'
a
$strB
EOC
# a
# $strB
```

**to file**

```bash
cat - << EOC > abc.txt
a
b
EOC
```

**to variable**

```bash
CODE=$(cat << EOC
a
b
EOC
)
echo "$CODE"
# a
# b
```
