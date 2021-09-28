## Scripting tips

`read` reads the input
    
`echo -n` doesn’t add a new line (doesn’t work in sh, instead: `\\c`)
    
`set -x` to print every comand 
    
`break` breaks the loop
    
`comm` to intersect two listsr
    
`read -r` to not read backslashes at the end of the string
    
Should always use ``“${BLA}”`` for the right interpolation
    
`pushd` and `popd` for changing directories
    
    
## Scripting tips from Pete    
If there are several arguments, they should be on their own lines
    
Be careful about directory cleanup
    
Syntax for calling subshell is `$(COMMAND)`  instead of  backtick because nesting
    
Exit with unique error codes to debug better
    
Use shellcheck 

## String interpolation

`$PATH$DIR`  -- concatenation (As opposed to put it in `${DIR}` inside the string: `PATH=”/bin/${DIR}”`)
    
Only double quotes are capable of string interpolation
    
If unquoted string variable is used as an argument to something else, then it will be broken down into different words
    
If a string may contain some special characters and so on, we should interpolate it -- put it in `“”` 
    
## Redirections 

* Redirect stdout to file: `pgm > file`
* Read file and put to stdin: `pgm < file`
* Append stdout output to file: `pgm >> file`
* Descriptor N redirects to file: `N > file`
* Descriptor N appends to file: `N >> file`
* Duplicate descriptor M as descriptor N: `N >& M`
* Duplicate descrptor M as descriptor N for input: `N <& M`
* Heredoc: 
```
<< EOF
... STUFF ...
EOF
```
More info: [http://www.tutorialspoint.com/unix/unix-io-redirections.htm](http://www.tutorialspoint.com/unix/unix-io-redirections.htm)  
## Bashisms

`*` in bash, when passed in a command means all files in a current directory 
    
`$?`  result of the last command
    
`$!` PID of the last process that was launched
    
Example: restart nginx every 12 hours

command: `"/bin/sh -c 'while :; do sleep 6h & wait $${!}; nginx -s reload; done & nginx -g \\"daemon off;\\"'"`  where `while :` means infinite loop; `$${!}` getting PID of the last process that was launched (so that we wait until the end of sleep)
        

## IF statements

`[ symlink_to_file_a -ef file_a ]` returns True
    
`\[ -z $STUFF \]` returns True if `$STUFF` is an empty string 
    