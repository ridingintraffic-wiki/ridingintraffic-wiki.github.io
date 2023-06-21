ripgrep is a line-oriented search tool that recursively searches the current directory for a regex pattern. By default, ripgrep will respect gitignore rules and automatically skip hidden files/directories and binary files.  
| command | Description |  
|----|---|  
| rg image utils.py	| Search in a single file utils.py  
| rg image src/	| Search in dir src/ recursively
| rg image | Search image in current dir recursively
| rg '^We' test.txt	| Regex searching support (lines starting with We)
| rg -i image	| Search image and ignore case (case-insensitive search)
| rg -s image	| Smart case search
| rg -F '(test)'	| Search literally, i.e., without using regular expression
| rg image -g '*.py'	| File globing (search in certain files), can be used multiple times
| rg image -g '!*.py'	| Negative file globing (do not search in certain files)
| rg image --type py or rg image -tpy1	| Search image in Python file
| rg image -Tpy	| Do not search image in Python file type
| rg -l image	| Only show files containing image (Do not show the lines)
| rg --files-without-match image	| Show files not containing image
| rg -v image	| Inverse search (search files not containing image)
| rg -w image	| Search complete word
| rg --count	| Show the number of matching lines in a file
| rg --count-matches	| Show the number of matchings in a file
| rg neovim --stats	|Show the searching stat (how many matches, how many files searched etc.)


How to exclude directories

To exclude directories, we also use the -g option. For example, to exclude dir1 and dir2, use the following command:  
```
rg pattern -g '!dir1/' -g '!dir2/'
```
