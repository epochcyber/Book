# sed Tool
SED command in UNIX stands for stream editor and it can perform lots of functions on file like searching, find and replace, insertion or deletion. Though most common use of SED command in UNIX is for substitution or for find and replace. By using SED you can edit files even without opening them.

### Basic Syntax
```bash
sed 's/pattern/replacement/' file.txt
```
- **s** : Substitute command.
- **pattern** : The regex pattern you’re looking for.
- **replacement** : The text that will replace the matched pattern.


### regular expression 
**1.1. Anchors**
-     ^ : Match the start of a line 
-     $ : Match the end of a line


**1.2. Wildcards**
-     . : Match any single character 
-     * : Match zero or more of the preceding character

**1.3. Character Classes**
-     [] : Match any one of the characters inside the brackets.

**1.4. word Boundaries**
-	  \<: Matches the start of a word.
-	  \>: Matches the end of a word.

**1.5. Groups and Backreferences: \( \) and \1, \2, etc**
-     \( \): Groups a portion of the pattern.
-     \1, \2, etc.: Refers to the content matched by each group.

**2. To apply changes directly to the file, use the -i option:**
```bash
sed -i 's/old/new/' file.txt
```

**3. flag in sed**
- **3.1. global**
```bash
sed 's/foo/bar/g' file.txt
```
- **3.2 Case-Insensitive (I or i)**
```bash
sed 's/hello/hi/I' file.txt
```
- **3.3 Escaping Special Characters**
If you want to match characters that have special meaning in regex (like /, *, ., &, etc.), you need to escape them using a backslash \
```bash
    sed 's/a\/b\/c/x\/y\/z/' file.txt
```

### now, we look some example of sed with regular expression
```bash
Replace “foo” with “bar” at the start of a line
    sed 's/^foo/bar/' file.txt

Remove all digits from a file
    sed 's/[0-9]//g' file.txt

Replace any sequence of spaces with a single space
    sed 's/ \+/ /g' file.txt
```
