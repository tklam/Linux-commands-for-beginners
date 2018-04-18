# Linux commands for beginners

The contents in this repository are based on:

- [TLDR pages](http://tldr.sh/)

This project aims to provide a brief reference of useful commands for Linux newbies.

## What is Linux? What is an operating system?
Please refer to these articles:

- [The history of Linux](http://linuxnewbieguide.org/overview-of-chapters/chapter-1-what-is-linux/)
- [Wikipedia](https://en.wikipedia.org/wiki/Linux)

## General Linux philosophies and rules

- Keep it simple, stupid (KISS) --- the utility programs (e.g. ls, cd) usually
  will report only when there have been some errors or the user is required to
  make decisions.
- Everything is a file --- a file is a file, a device(e.g. USB memory stick) is also a file.

## Command line
The user interacts with the system via a *terminal*, which is an interface for sending commands to
the system. The terminal can be seen as a client program for the user to connect to the server
system either locally or remotely.

After logging in the system, the user works with the *shell*. It is a program and a part of the
operating system for actually interpreting and executing commands from the user. There are many
shells available to choose from. One of the most popular shell nowadays is called *bash*.

## Using bash
### Shortcuts in *bash* shell
- Command completion:
`<tab>`

- Previous command in the history:
`<up>`

- Next command in the history:
`<down>`

- Search previous command:
`<ctrl> r`

- Move the cursor to the beginning of the next word:
`<alt> f`

- Move the cursor to the beginning of the previous word:
`<alt> b`

- Delete the rest of the command line from the cursor:
`<ctrl> k`

- Delete until the beginning of the next word:
`<alt> d`

### Getting information about a command
#### man

> Format and display manual pages.

- Display man page for a command:

`man {{command}}`

- Display path searched for manpages:

`man --path`

- Display location of a manpage rather than the manpage itself:

`man -w {{command}}`

- Do a keyword search for manpages containing a search string:

`man -k {{keyword}}`

### Redirection (more advanced)
Please refer to [Redirection](ttps://en.wikipedia.org/wiki/Redirection_(computing))

Every command/program has 3 *streams*:

- standard input --- stdin, what user types
- standard output --- stdout, what a command prints (normal mode)
- standard error --- stderr, , what a command prints (error mode)

Most commonly used commands:

- `>` --- redirects stdout to a file. The file will be overwritten.
- `>>` --- redirects stdout to a file. The output from stdout will be appended to the
  file.
- `<` --- redirects a file to stdin (read from a file as if the content is typed by
  the user)
- `2>` --- redirects stderr to a file
- `|` --- Known as the *pipe*. Redirects the output of a command as the input of
  another command.


## Navigation
### Where are we?
#### pwd

> Print name of current/working directory.

- Print the current directory:

`pwd`

- Print the current directory, and resolve all symlinks (i.e. show the "physical" path of shortcuts):

`pwd -P`

### Some special places in Linux (bash)
- */* --- the *root* directory, which is the base of the system
- *./* --- the *current* directory
- *../* --- the parent directory of a directory (one level closer to `/`
- *../../* --- the parent directory of the parent directory of a directory 
- *../../../* --- (you guess what this means)
- *~/*  --- the home directory of the user, which is usually `/home/<username>/`

We can specify the path to a directory by either a *relative path* or an *absolute
path* or a shortcut. For example, suppose our username is venom and we are at
the directory `/home/venom/experiment/toxic/`, we can specify
`/home/venom/experiment/` by any one of the following ways:

- `../` -- one level closer to /
- `/home/venom/experiment/`
- `~/experiment/`
- `/home/venom/experiment/toxic/../`
- `/home/venom/experiment/toxic/../toxic/../`
- `/home/venom/experiment/toxic/123/../../`
- and many other ways

The trailing slash can sometimes be omitted.

### What's inside a directory?
#### ls

> List directory contents.

- List files one per line:

`ls -1 {{path/to/directory}}`

- List all files, including *hidden files*:

`ls -a {{path/to/directory}}`

- Long format list (permissions, ownership, size and modification date) of all files:

`ls -la {{path/to/directory}}`

- Long format list with size displayed using human readable units (KB, MB, GB):

`ls -lh {{path/to/directory}}`

- Long format list sorted by size (descending):

`ls -lS {{path/to/directory}}`

- Long format list of all files, sorted by modification date (oldest first):

`ls -ltr {{path/to/directory}}`

### Change directory
#### cd

> Change the current working directory.

- Go to the given directory:

`cd {{path/to/directory}}`

- Go to home directory of current user:

`cd`

- Go up to the parent of the current directory:

`cd ..`

- Go to the previously chosen directory:

`cd -`


## File manipulation
### Properties the file system
- Extensionless --- every file can be an executable, a library, an image, an
  audio file or anything else regardless of whatever the suffix of the filename is.

- Case sensitive

### Getting information about a file
#### file

> Determine file type.

- Give a description of the type of the specified file. Works fine for files
  with no file extension:

`file {{filename}}`

- Look inside a zipped file and determine the file type(s) inside:

`file -z {{foo.zip}}`

- Allow file to work with special or device files:

`file -s {{filename}}`

- Don't stop at first file type match; keep going until the end of the file:

`file -k {{filename}}`

- Determine the mime encoding type of a file:

`file -i {{filename}}`

### Dealing with files and directories
#### cp

> Copy files and directories.

- Copy a file to another location with a new name:

`cp {{path/to/file.ext}} {{path/to/copy.ext}}`

- Copy a file into another directory, keeping the filename:

`cp {{path/to/file.ext}} {{path/to/target/parent/directory/}}`

- Copy a directory recursively to another location:

`cp -r {{path/to/directory}} {{path/to/copy}}`

- Copy a directory recursively into another directory, keeping the directory
  name:

`cp -r {{path/to/directory}} {{path/to/target/parent/directory}}`

- Copy a directory recursively with a new name, in verbose mode (shows files as
  they are copied):

`cp -vr {{path/to/directory}} {{path/to/copy}}`

- Copy the contents of a directory into another directory:

`cp -r {{path/to/source/directory/*}} {{path/to/target/directory/}}`

- Copy text files to another location, in interactive mode (prompts user before
  overwriting):

`cp -i {{*.txt}} {{path/to/source/}}`

#### rm

> Remove files or directories.

- Remove files from arbitrary locations:

`rm {{path/to/file}} {{path/to/another/file}}`

- Recursively remove a directory and all its subdirectories:

`rm -r {{path/to/directory}}`

- Forcibly remove a directory, without prompting for confirmation or showing
  error messages:

`rm -rf {{path/to/directory}}`

- Interactively remove multiple files, with a prompt before every removal:

`rm -i {{file(s)}}`

- Remove files in verbose mode, printing a message for each removed file:

`rm -v {{path/to/directory/*}}`


#### mv

> Move or rename files and directories.

- Move files in arbitrary locations:

`mv {{source}} {{target}}`

- Do not prompt for confirmation before overwriting existing files:

`mv -f {{source}} {{target}}`

- Do not prompt for confirmation before overwriting existing files but write to
  standard error before overriding:

`mv -fi {{source}} {{target}}`

- Move files in verbose mode, showing files after they are moved:

`mv -v {{source}} {{target}}`

#### mkdir

> Creates a directory.

- Create a directory in current folder or given path:

`mkdir {{directory}}`

- Create directories recursively (useful for creating nested dirs):

`mkdir -p {{path/to/directory}}`


### Wilecards/regular expressions
> Commands can use wildcards/regular expressions to perform actions on more than
> one file at a time, or to find part of a phrase in a text file.

We can use wildcards at any part of a path to specify a set of files. The set of
wildcards supported by Linux:

- `*` --- zero or more characters
- `?` --- one character
- `[]` --- one character in a set of characters

For details, please refer to [Wildcards](http://tldp.org/LDP/GNU-Linux-Tools-Summary/html/x11655.htm).

Examples:

- Display information about every file in the current directory:

`file *`

- List all files that ends with .html or .txt:

`ls *.html *.txt`

- Display information about every file in the current directory if the filename
  has exactly 3 characters:

`file ???`

- List all files in the current directory that have a three-character filename
  suffix after a dot:

`ls *.???`

- Display information about every file in the current directory if the filename
  contains x, y or z:

`file *[xyz]*`

- List all files whose filename starts with venom and ends with three single
  digit numbers:

`ls venom[0-9][0-9][0-9]`

- List all files whose filename starts with any character in a-z:

`ls [a-z]*`

- List all files whose filename does not start with c, u, h or k:

`ls [^cuhk]*`

### Permissions
> File systems use permissions and attributes to regulate the level of
> interaction that system processes can have with files and directories. 

Please refer to [File permissions and attributes](https://wiki.archlinux.org/index.php/File_permissions_and_attributes).

#### chmod

> Change the access permissions of a file or directory.

- Give the [u]ser who owns a file the right to e[x]ecute it:

`chmod u+x {{file}}`

- Give the user rights to [r]ead and [w]rite to a file/directory:

`chmod u+rw {{file}}`

- Remove executable rights from the [g]roup:

`chmod g-x {{file}}`

- Give [a]ll users rights to read and execute:

`chmod a+rx {{file}}`

- Give [o]thers (not in the file owner's group) the same rights as the group:

`chmod o=g {{file}}`

- Change permissions recursively giving [g]roup and [o]thers the ability to
  [w]rite:

`chmod -R g+w,o+w {{directory}}`

### Some useful uUtilities
#### cat

> Print and concatenate files.

- Print the contents of a file to the standard output:

`cat {{file}}`

- Concatenate several files into the target file:

`cat {{file1}} {{file2}} > {{target_file}}`

- Append several files into the target file:

`cat {{file1}} {{file2}} >> {{target_file}}`

- Number all output lines:

`cat -n {{file}}`

#### tail

> Display the last part of a file.

- Show last 'num' lines in file:

`tail -n {{num}} {{file}}`

- Show all file since line 'num':

`tail -n +{{num}} {{file}}`

- Show last 'num' bytes in file:

`tail -c {{num}} {{file}}`

- Keep reading file until `<ctrl> c`:

`tail -f {{file}}`

- Keep reading file until `<ctrl> c`, even if the file is rotated:

`tail -F {{file}}`

#### head
`head` is similar to `tail`, but show the first n part of a file.

#### sort

> Sort lines of text files.

- Sort a file in ascending order:

`sort {{filename}}`

- Sort a file in descending order:

`sort -r {{filename}}`

- Sort a file using numeric rather than alphabetic order:

`sort -n {{filename}}`

- Sort the passwd file by the 3rd field, numerically:

`sort -t: -k 3n /etc/passwd`

- Sort a file preserving only unique lines:

`sort -u {{filename}}`

#### wc

> Count words, bytes, or lines.

- Count lines in file:

`wc -l {{file}}`

- Count words in file:

`wc -w {{file}}`

- Count characters (bytes) in file:

`wc -c {{file}}`

- Count characters in file (taking multi-byte character sets into account):

`wc -m {{file}}`

#### diff

> Compare files and directories.

- Compare files:

`diff {{file1}} {{file2}}`

- Compare files, ignoring white spaces:

`diff -w {{file1}} {{file2}}`

- Compare files, showing differences side by side:

`diff -y {{file1}} {{file2}}`

- Compare directories recursively:

`diff -r {{directory1}} {{directory2}}`

- Compare directories, only showing the names of files that differ:

`diff -rq {{directory1}} {{directory2}}`


#### grep (more advanced)

> Matches patterns in input text.
> Supports simple patterns and regular expressions.

- Search for an exact string:

`grep {{search_string}} {{path/to/file}}`

- Search in case-insensitive mode:

`grep -i {{search_string}} {{path/to/file}}`

- Search recursively (ignoring non-text files) in current directory for an exact
  string:

`grep -rI {{search_string}} .`

- Use extended regular expressions (supporting `?`, `+`, `{}`, `()` and `|`):

`grep -E {{^regex$}} {{path/to/file}}`

- Print 3 lines of [C]ontext around, [B]efore, or [A]fter each match:

`grep -{{C|B|A}} 3 {{search_string}} {{path/to/file}}`

- Print file name with the corresponding line number for each match:

`grep -Hn {{search_string}} {{path/to/file}}`

- Use the standard input instead of a file:

`cat {{path/to/file}} | grep {{search_string}}`

- Invert match for excluding specific strings:

`grep -v {{search_string}}`

Please study [Regular Expressions](https://www.ibm.com/developerworks/library/l-lpic1-103-7/)
before learning `grep`, `sed` and `awk`.


#### sed (more advanced)

> Run replacements based on regular expressions.

- Replace the first occurrence of a string in a file, and print the result:

`sed 's/{{find}}/{{replace}}/' {{filename}}`

- Replace all occurrences of a string in a file, and print the result:

`sed 's/{{find}}/{{replace}}/g' {{filename}}`

- Replace all occurrences of an extended regular expression in a file:

`sed -r 's/{{regex}}/{{replace}}/g' {{filename}}`

- Replace all occurrences of a string in a file, overwriting the file (i.e. in-place):

`sed -i 's/{{find}}/{{replace}}/g' {{filename}}`

- Replace only on lines matching the line pattern:

`sed '/{{line_pattern}}/s/{{find}}/{{replace}}/' {{filename}}`

- Apply multiple find-replace expressions to a file:

`sed -e 's/{{find}}/{{replace}}/' -e 's/{{find}}/{{replace}}/' {{filename}}`

- Replace separator / by any other character not used in the find or replace patterns, e.g., #:

`sed 's#{{find}}#{{replace}}#' {{filename}}`

#### awk (more advanced)

> A versatile programming language for working on files.

- Print the fifth column (a.k.a. field) in a space-separated file:

`awk '{print $5}' {{filename}}`

- Print the second column of the lines containing "something" in a space-separated file:

`awk '/{{something}}/ {print $2}' {{filename}}`

- Print the last column of each line in a file, using a comma (instead of space) as a field separator:

`awk -F ',' '{print $NF}' {{filename}}`

- Sum the values in the first column of a file and print the total:

`awk '{s+=$1} END {print s}' {{filename}}`

- Sum the values in the first column and pretty-print the values and then the total:

`awk '{s+=$1; print $1} END {print "--------"; print s}' {{filename}}`

- Print every third line starting from the first line:

`awk 'NR%3==1' {{filename}}`

## Process management
It is easy to manage a process in Linux using command line. We can control
whether a process run in the foreground or background of the shell, and whether
it should be killed.

A foreground process in the shell is a running command that blocks the user from
entering new commands into the shell. On the other hand, a background process
can run without blocking the shell input.

### Getting information about a process
Every process has a *process ID* (PID). We can use `top` or `ps` to get the
the info as well as the process IDs of the processes running on the system.

#### ps

> Information about running processes.

- List all running processes:

`ps aux`

- List all running processes including the full command string:

`ps auxww`

- Search for a process that matches a string:

`ps aux | grep {{string}}`

- List all processes of the current user in extra full format:

`ps --user $(id -u) -F`

- List all processes of the current user as a tree:

`ps --user $(id -u) f`

- Get the parent pid of a process:

`ps -o ppid= -p {{pid}}`

### Controlling a process
#### `<ctrl> c`
Kill a process running in the foreground. (It is possible that `<ctrl> c` is not
able to kill a process, especially the process is not a core utility.)

#### kill

> Sends a signal to a process, usually related to stopping the process.
> All signals except for SIGKILL and SIGSTOP can be intercepted by the process
> to perform a clean exit.

- Terminate a program using the default SIGTERM (terminate) signal:

`kill {{process_id}}`

- List available signal names (to be used without the `SIG` prefix):

`kill -l`

- Terminate a program using the SIGHUP (hang up) signal. Many daemons will
  reload instead of terminating:

`kill -{{1|HUP}} {{process_id}}`

- Terminate a program using the SIGINT (interrupt) signal. This is typically
  initiated by the user pressing `Ctrl + C`:

`kill -{{2|INT}} {{process_id}}`

- Signal the operating system to immediately terminate a program (which gets no
  chance to capture the signal):

`kill -{{9|KILL}} {{process_id}}`

- Signal the operating system to pause a program, it until a SIGCONT
  ("continue") signal is received:

`kill -{{17|STOP}} {{process_id}}`


#### killall

> Send kill signal to all instances of a process by name (must be exact name).
> All signals except SIGKILL and SIGSTOP can be intercepted by the process,
> allowing a clean exit.

- Terminate a process using the default SIGTERM (terminate) signal:

`killall {{process_name}}`

- List available signal names (to be used without the 'SIG' prefix):

`killall --list`

- Interactively ask for confirmation before termination:

`killall -i {{process_name}}`

- Terminate a process using the SIGINT (interrupt) signal, which is the same
  signal sent by pressing `Ctrl + C`:

`killall -INT {{process_name}}`

- Force kill a process:

`killall -KILL {{process_name}}`

#### jobs

> Display status of jobs in the current session.

- Show status of all jobs:

`jobs`

- Show status of a particular job:

`jobs {{job_id}}`

- Show status and process IDs of all jobs:

`jobs -l`

- Show process IDs of all jobs:

`jobs -p`


#### &
Start a job in the background.


#### `<ctrl> z`
Suspend a job.

#### bg

> Resumes jobs that have been suspended (e.g. using `<ctrl>  z`), and keeps them
> running in the background.

- Resume most recently suspended job and run it in the background:

`bg`

- Resume a specific job (use `jobs -l` to get its ID) and run it in the background:

`bg {{job_id}}`


#### fg

> Run jobs in foreground.

- Bring most recently suspended background job to foreground:

`fg`

- Bring a specific job to foreground:

`fg {{job_id}}`

#### screen
All jobs in the foreground and background will be terminated when the user
logout. We can use `screen` to let a job continue to run on the server.

> Hold a session open on a server.

- Start a new screen session:

`screen`

- Start a new named screen session:

`screen -S {{session_name}}`

- Show open screen sessions:

`screen -ls`

- Reattach to an open screen:

`screen -r {{session_name}}`

- Detach from inside a screen:

`<ctrl>  a d`

## bash scripting (more advanced)
Please refer to [Wikibooks](https://en.wikibooks.org/wiki/Bash_Shell_Scripting).

## Using Vi IMproved (vim, an editor)
#### vim

> Vi IMproved, a programmer's text editor, providing several modes for different kinds of text manipulation.
> Pressing `i` enters edit mode. `<Esc>` goes back to normal mode, which doesn't allow regular text insertion.

- Open a file:

`vim {{file}}`

- Enter text editing mode (insert mode):

`<Esc>i`

- Copy ("yank") or cut ("delete") the current line (paste it with `P`):

`<Esc>{{yy|dd}}`

- Undo the last operation:

`<Esc>u`

- Search for a pattern in the file (press `n`/`N` to go to next/previous match):

`<Esc>/{{search_pattern}}<Enter>`

- Perform a regex substitution in the whole file:

`<Esc>:%s/{{pattern}}/{{replacement}}/g<Enter>`

- Save (write) the file, and quit:

`<Esc>:wq<Enter>`

- Quit without saving:

`<Esc>:q!<Enter>`
