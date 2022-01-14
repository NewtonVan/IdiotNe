---
title: Linux Command Line
date: 2019-08-11 11:14:50
tags: Operating System
categories: Programming
---


# Learning Shell
***

## About Shell
***

When we speak of command line, we are referring to the shell. The shell is a program that takes keyboard commands and passes them to the operating system to carry out. Almost all linux distribtuions supply a shell program from the GNU project called bash, which is an acronym for "Bourne Again Shell"

When using a graphical user interface, we need another program called a terminal emulator to interact with shell.

## Navigate the File System  
***

* pwd - print working directory
* ls - list the files and the directories in the current working directory, we use the ls command line.
* cd [pathname]- change the working directory.
* cd - change the working directory to your home directory.
* "cd -" - change the working directory to the previous working directory.
* cd ~username - change the working directory to the home directory user_name.

### Absolute Pathname
***

An absolute pathname begins with the root directory and follows with branch by branch until the path to the desired directory and file is completed.

### Relative Pathname
***

We use "." and ".." to represent relative positions in the file system tree.
The "." symbol refers to the working directory and the ".." refers to the working directory's parent directory.

In almost all cases, you can omit the "./". It is implied.

### Important Facts About Filenames
***

*  Filenames that begin with a period character "." are hidden. That only means that ls will not list them unless you use "ls-a".
*  Filenames and commands in linux, like unix, are case sensitive.
*  Linux has no concept of a "file extension" like some other operating systems.
*  Though Linux supports long filenames which may contain embedded spaces and punctuation characters, limit the punctuation characters in the name of files you create to period, dash, and underscore. 


## Exploring your System
***

### The fun of ls
***

* We can specify the directory to list. 
* Even specify multiple directories.

### Options and Arguments
***

| Options | long option| Description|
|---|---|---|
|-a| --all| List all files, even thos with name begin with a period, which are normally not list.|
|-d| --directory | Ordinarily, if a directory is not specified, ls will list the contents of the directory, not the directory itself. Use this option conjunction with the -l option to see details about the directory rather than its contents.|
|-F| --classify| This option will append an indicator character to the end of each listed name. For example, a '/' if the name is a directory.|
|-h| --human-readable| In long format listings, display sizes in human readable format rather than in bytes.|
|-l| | Display result in long format.|
|-r| --reverse| Display the result in reverse order. Normally, ls display its results in ascending alphabetical order.|
|-S| | Sort results by file size.|
|-t | | Sort by modification time.|

### Useful Information From Long Format
***

Take an example directory from Ubuntu:
> -rw-r--r-- 1 root root   32059 2007-04-03 11:05 oo-cd-cover.odf

Look at the different fields from this file and examine their meanings:
| Field | Meaning |
|---|---|
| -rw-r--r-- | Access rights to file. The first character indicates the type of file. Among the different types, a leading dash means a regular file, while a "d" indicates a directory. The next three characters are the access rights for the file's owner, the next three are for the members of the file's group, and the final three are for the everyone else. The full meaning of this is discussed in chapter Permissions.|
| l | File's number of hard links. |
| root | The user name of the file's owner. |
| root | The name of the group which owns the file.| 
| 32059 | Size of the file in bytes. |
|2007-04-03 11:05 | Date and time of the last modification|
| oo-cd-cover.odf | Name of the file. |

### Confirm the Type Of the File
***

We can invoke the file command this way:
>file [filename]


### View Text Files with Less
***

* less [filename]

| Command of less mode | Action |
|---|---|
|PAGE UP or b| Scroll back one page |
|PAGE DOWN or space | Scorll forward one page |
| UP Arrow | Scroll Up one line |
| Down Arrow | Scroll down one line |
| G | Move to the end of the text file |
| lG or g| Move to the beginning of the text file |
| /[characters] | Search forward for the next occurance of characters |
| n | Search forward for the next occurance of the previous search |
| h | Display help screen |
| q | Quit less mode |

### Copy and Paste Trick
***

Double click on a file name and middle click to paste it into commands.

### Wandering Around the File System
***

| Drectory | Comments |
|---|---|
| / | The root directory. Where everything begins. |
| /bin | Contains binaries(program) that must be present for the system to boot and run. |
| /boot | Contains the linux kernel, initial RAM disk image(for drivers' needed at boot time), and the boot loader.  |
| /dev | This is a special directory which contains device nodes. Here is where the kernel maintains a list of all the devices it understand. |
| /etc | The etc directory contains all the system-wide configuration files. It also contains a collection of shell scripts which start each of the system devices at boot time. Everything in this directory should be readable text files. |
| /home | In normal configurations, each user is given a directory in /home. Ordinary users can only write their files in their home directories. This limitation protects system from errant user activity. |
| /lib | Contained shared library files used by the core system programs. These are similar to DLL in windows. |
| /lost+found | Each formatted partition or device using a linux file system, such as ext3, will have this directory. It is used in the case of a partial recovery from a file system corruption event. Unless something really bad has happened to your system, this directroy will remain empty. |
| /media | On modern Linux systems the /media directory will contain the mount points for removable media such USB drives, CD-ROMs, etc. that are mounted automatically at insertion. |
| /mnt | On older Linux systems, the /mnt directory contains mount points for removable devices that have been mounted manually. |
| /opt | The /opt directory is used to install “optional” software. This is mainly used to hold commercial software products that may be installed on your system. |
| /proc | The /proc directory is special. It's not a real file system in the sense of files stored on your hard drive. Rather, it is a virtual file system maintained by the Linux kernel. The “files” it contains are peepholes into the kernel itself. The files are readable and will give you a picture of how the kernel sees your computer. |
| /root | This is the home directory for the root account. |
| /sbin | This directory contains “system” binaries. These are programs that perform vital system tasks that are generally reserved for the superuser. |
| /tmp | The /tmp directory is intended for storage of temporary, transient files created by various programs. Some configurations cause this directory to be emptied each time the system is rebooted. |
| /usr | The /usr directory tree is likely the largest one on a Linux system. It contains all the programs and support files used by regular users. |
| /usr/bin | /usr/bin contains the executable programs installed by your Linux distribution. It is not uncommon for this directory to hold thousands of programs. |
| /usr/lib | The shared libraries for the programs in /usr/bin. |
| /usr/local | The /usr/local tree is where programs that are not included with your distribution but are intended for system- wide use are installed. Programs compiled from source code are normally installed in /usr/local/bin. On a newly installed Linux system, this tree exists, but it will be empty until the system administrator puts something in it. |
| /usr/sbin | Contains more system administration programs. |
| /usr/share | /usr/share contains all the shared data used by programs in /usr/bin. This includes things like default configuration files, icons, screen backgrounds, sound files, etc. |
| /usr/share/doc |      Most packages installed on the system will include some kind of documentation. In /usr/share/doc, we will find documentation files organized by package. |
| /var | With the exception of /tmp and /home, the directories we have looked at so far remain relatively static, that is, their contents don't change. The /var directory tree is where data that is likely to change is stored. Various databases, spool files, user mail, etc. are located here. |
| /var/log | /var/log contains log files, records of various system activity. These are very important and should be monitored from time to time. The most useful one is /var/log/messages. Note that for security reasons on some systems, you must be the superuser to view log files. |

### Symbolic links
***

In most Unix-like system, it is possible to have a file referenced by multiple names.  


## Manipulating System
***

### Wildcard
***

| Wildcard | Meaning |
|---|---|
| * | Matches any characters. |
| ? | Match any single character. |
| [characters] | Matches any character that is a member of the set characters. |[!characters] | Matches any character that is not a member of the set characters. |
| [[:class:]] | Matches any character that is a member of the specified class. |

| Character class | Meaning |
|---|---|
| [:alnum:] | Matches any alphanumeric character. |
| [:alpha:] | Matches any alphabetic character. |
| [:digit:] | Matches any numeral. |
| [:lower:] | Matches any lowercase letter. |
| [:upper:] | Matches any uppercase letter. |

### mkdir
***

Create a new file by this command. 
` mkdir [filename]...`

We can create more than one file one time.

### cp- copy the file or the directory
***

`cp item1 item2`
`cp [item]... [directory]`

We can copy one item or multiple items into the target file.

### Useful Option For cp
*** 

| Option | Meaning |
|---|---|
| -a, --archive |   Copy the files and directories and all of their attributes, including ownerships and permissions. Normally, copies take on the default attributes of the user performing the copy. |
| -i, --interactive |   Before overwriting an existing file, prompt the user for confirmation. If this option is not specified, cp will silently overwrite files. |
| -r, --recursive | Recursively copy directories and their contents. This option (or the -a option) is required when copying directories. |
| -u, --update | When copying files from one directory to another, only copy files that either don't exist, or are newer than the existing corresponding files, in the destination directory. |
| -v, --verbose | Display informative messages as the copy is performed. |

### mv- move and rename the file
*** 

`mv item1 item2`

Move or rename the "item1" to "item2".

`mv [item]... [directory]`

Move one or more items from one directory to another.

### Useful option For mv
***

| Option | Meaning |
|---|---|
| -i --interactive | Before overwriting an existing file, prompt the user for confirmation. If this option is not specified, mv command will silently overwrite files. |
| -u --update | When moving files from one directory to another, only move files that either don't exist, or are newer than the existing corresponding files in the destination directory. |
| -v --verbose | Display informative messages as the move is performed. |

### rm-!!!
*** 

>rm item...

Remove the item by this command.

### Useful option for rm
***

| Option | Meaning |
|---|---|
| -i, --interactive | Before deleting an existing file, prompt the user for confirmation. If this option is not specified, rm will silently delete files. |
| -r, --recursive | Recursively delete directories. This means that if a directory being deleted has subdirectories, delete them too. To delete a directory, this option must be specified. |
| -f, --force | Ignore nonexistent files and do not prompt. This overrides the --interactive option. |
| -v, --verbose | Display informative messages as the deletion is performed. |


Before you use wildcards with rm, besides carefully checking your spelling, you'd better use ls to examine the file or directory you are going to remove.

### ln- create links
***

It is used to create hard or symbolic links. 

Create a hard link:

>ln file link

Create a symbolic link:

>ln -s item link

### What is hard link
***

Hard links are the original Unix way of creating links; symbolic links are more modern. By default, every file has a single hard link that gives the file its name. When we create a hard link, we create an additional directory entry for a file. 

Here are the two limitation of hard link:

* A hard link cannot reference a file outside its own file system. This means a link may not reference a file that is not on the same disk partition as the link itself.
* A hard link may not reference a directory.

A hard link is indistinguishable from the file itself. Unlike a symbolic link, when you list a directory containing a hard link you will see no special indication of the link. When a hard link is deleted, the link is removed but the contents of the file itself continue to exist (that is, its space is not deallocated) until all links to the file are deleted.

### Symbolic link
***

Symbolic links were created to overcome the limitations of hard links. Symbolic links work by creating a special type of file that contains a text pointer to the referenced file or directory. In this regard, they operate in much the same way as a Windows shortcut though of course.

A file pointed to by a symbolic link, and the symbolic link itself are largely indistinguishable from one another. For example, if you write some something to the symbolic link, the referenced file is also written to. However when you delete a symbolic link, only the link is deleted, not the file itself. If the file is deleted before the symbolic link, the link will continue to exist, but will point to nothing. In this case, the link is said to be broken. In many implementations, the ls command will display broken links in a distinguishing color, such as red, to reveal their presence.

### Creating Symlinks with GUI
***

The file managers in both GNOME and KDE provide an easy and automatic method of creating symbolic links. With GNOME, holding the Ctrl+Shift keys while dragging a file will create a link rather than copying (or moving) the file. In KDE, a small menu appears whenever a file is dropped, offering a choice of copying, moving, or linking the file.

## Using Command
***

What is command?

* An executable program like all those files we saw in /usr/bin. Within this category, programs can be compiled binaries such as programs written in C and C++, or programs written in scripting languages such as the shell, perl, python, ruby, etc.
* A command built into the shell itself. bash supports a number of commands internally called shell builtins. The cd command, for example, is a shell builtin.
* A shell function. These are miniature shell scripts incorporated into the environment. We will cover configuring the environment and writing shell functions in later chapters.
* An alias. Commands that we can define ourselves, built from other commands.

### type - show the type of the command
***

The type command is a shell builtin that displays the kind of command the shell will execute, given a particular command name.

`type [command]`


### which - show the position of executable program.
***

which only works for executable programs, not builtins nor aliases that are substitutes for actual executable programs.

To determine the exact location of a given executable, the which command is used:
`which [command]`

### help-get the document of the builtins for the shell 
***

Bash has a built-in help facility available for each of the shell builtins. To use it, type “help” followed by the name of the shell builtin.
`help [command]`

A note on notation: When square brackets appear in the description of a command’s syntax, they indicate optional items. A vertical bar character indicates mutually exclusive items.

### --help - show the information of command
***

Many executable programs support a “--help” option that displays a description of the command’s supported syntax and options.

`[command] --help`

### man - call for the documentation called man page / manual page 
***

`man [command]`

On most Linux systems, man uses less to display the manual page, so all of the familiar less commands work while displaying the page.

The “manual” that man displays is broken into sections and not only covers user commands but also system administration commands, programming interfaces, file formats and more. 

| Section | Contents |
|---|---|
| 1 | User commands |
| 2 | Programming interfaces kernel system calls |
| 3 | Programming interfaces to the C library |
| 4 | Special files such as device nodes and drivers |
| 5 | File formats |
| 6 | Games and amusements such as screen savers |
| 7 | Miscellaneous |
| 8 | System administration commands |

Sometimes we need to look in a specific section of the manual to find what we are looking for. This is particularly true if we are looking for a file format that is also the name of a command. Without specifying a section number, we will always get the first instance of a match, probably in section 1.

### apropos - show the proper command
***

`apropos [keyword]`
The first field in each line of output is the name of the man page, the second field shows the section. Note that the man command with the “-k” option performs the exact same function as apropos.

### whatis - very simple introduction
***

The whatis program displays the name and a one line description of a man page matching a specified keyword.

### info - show the contents of program
***

The GNU Project provides an alternative to man pages for their programs, called “info.” Info pages are displayed with a reader program named, appropriately enough, info. Info pages are hyperlinked much like web pages. 

The info program reads info files, which are tree structured into individual nodes, each containing a single topic. Info files contain hyperlinks that can move you from node to node. A hyperlink can be identified by its leading asterisk, and is activated by placing the cursor upon it and pressing the enter key.

To invoke info, type “info” followed optionally by the name of a program. Below is a table of commands used to control the reader while displaying an info page.

| Commands | Action |
|---|---|
| ? | Display command help |
| PageUp or Backspace | Display privious page |
| PgDn or Space | Display next page |
| n | Display next node |
| p | Previous - Display the previous node |
| u | Up - Display the parent node of the currently displayed node, usually a menu.|
| Enter | Follow the hyperlink at the cursor location |
| q | quit |

Most of the command line programs we have discussed so far are part of the GNU Project’s “coreutils” package. So typing:

`info coreutils`

will display a menu page with hyperlinks to each program contained in the coreutils package.

### alias - create your own command 
***

Now for our very first experience with programming! We will create a command of our own using the alias command. But before we start, we need to reveal a small command line trick. It’s possible to put more than one command on a line by separating each command with a semicolon character.

Now let’s turn this sequence into a new command using alias. The first thing we have to do is dream up a name for our new command. Let’s try “test”. Before we do that, it would be a good idea to find out if the name “test” is already being used. 

To create our alias:
`alias [your command]= "[the command string]" `

After the command “alias” we give alias a name followed immediately (no whitespace allowed) by an equals sign, followed immediately by a quoted string containing the meaning to be assigned to the name. After we define our alias, it can be used anywhere the shell would expect a command. 

To remove an alias, the unalias command is used, like so:

`unalias [your command]`

To see all the aliases defined in the environment, use the alias command without arguments. Here are some of the aliases defined by default on a Fedora system. 

There is one tiny problem with defining aliases on the command line. They vanish when your shell session ends. 


## Redirection
***

### stdin, stdout, stderr
***

Many of the programs that we have used so far produce output of some kind. This output often consists of two types. First, we have the program’s results; that is, the data the program is designed to produce, and second, we have status and error messages that tell us how the program is getting along. 

Keeping with the Unix theme of “everything is a file,” programs such as ls actually send their results to a special file called standard output (often expressed as stdout) and their status messages to another file called standard error (stderr). By default, both standard output and standard error are linked to the screen and not saved into a disk file. In addition, many programs take input from a facility called standard input (stdin) which is, by default, attached to the keyboard.

I/O redirection allows us to redefine where standard output goes. To redirect standard output to another file besides the screen, we use the “>” redirection operator followed by the name of the file. It’s often useful to store the output of a command in a file. For example, we could tell the shell to send the output of the ls command to the file ls-output.txt instead of the screen

### stdout redirection
***

When we redirect output with the “>” redirection operator, the destination file is always rewritten from the beginning.

In fact, if we ever need to actually truncate a file (or create a new, empty file) we can use a trick like this:

`> [filename]`

We can append redirected output to a file instead overwriting the file from the file in this way:

`[stdout needed to be redirected] >> [destination]`

Using the “>>” operator will result in the output being appended to the file. If the file does not already exist, it is created just as though the “>” operator had been used. 

###  stderr redirection
***

Redirecting standard error lacks the ease of a dedicated redirection operator. To redirect standard error we must refer to its file descriptor. A program can produce output on any of several numbered file streams. While we have referred to the first three of these file streams as standard input, output and error, the shell references them internally as file descriptors zero, one and two, respectively. The shell provides a notation for redirecting files using the file descriptor number. 

`[stderr needed to be redirected] 2> [destination]`

The file descriptor “2” is placed immediately before the redirection operator to perform the redirection of standard error to the file.

### stdout & stderr redirection
***

There are cases in which we may wish to capture all of the output of a command to a single file. To do this, we must redirect both standard output and standard error at the same time. There are two ways to do this. First, the traditional way, which works with old versions of the shell:

`[content needed to be redirected] > [destination] 2>&1`

Using this method, we perform two redirections. First we redirect standard output to the file  and then we redirect file descriptor two (standard error) to file descriptor one (standard output) using the notation 2>&1.

Notice that the order of the redirections is significant. The redirection of standard error must always occur after redirecting standard output or it doesn’t work.

Recent versions of bash provide a second, more streamlined method for performing this combined redirection:

`[content needed to be redirected] &> [destination]`

In this example, we use the single notation &> to redirect both standard output and standard error to the file.

### Handle with the meaningless output
***

Sometimes “silence is golden,” and we don’t want output from a command, we just want to throw it away. This applies particularly to error and status messages. The system provides a way to do this by redirecting output to a special file called “/dev/null”. This file is a system device called a bit bucket which accepts input and does nothing with it. To suppress error messages from a command, we do this:

`[rubbish information] 2> /dev/null`

### cat- concatenate
***

The cat command reads one or more files and copies them to standard output like so:

`cat [file]`

In most cases, you can think of cat as being analogous to the TYPE command in DOS. You can use it to display files without paging.

If cat is not given any arguments, it reads from standard input and since standard input is, by default, attached to the keyboard, it’s waiting for us to type something.

After you typed something, type a Ctrl-d (i.e., hold down the Ctrl key and press “d”) to tell cat that it has reached end of file (EOF) on standard input.
In the absence of filename arguments, cat copies standard input to standard output, so we see our line of text repeated. 

We can play cat in this way:

`cat > [file]`

Type the command followed by the text we want in to place in the file. Remember to type Ctrl-d at the end. 

Using the “<” redirection operator, we change the source of standard input from the keyboard to the file. 

### | - Pipe Line
***

The ability of commands to read data from standard input and send to standard output is utilized by a shell feature called pipelines. Using the pipe operator “|” (vertical bar), the standard output of one command can be piped into the standard input of another. 

`command1 | command2`

### Filters
***

Pipelines are often used to perform complex operations on data. It is possible to put several commands together into a pipeline. Frequently, the commands used this way are referred to as filters. 

### uniq - report or ingore duplicates
***

The uniq command is often used in conjunction with sort. uniq accepts a sorted list of data from either standard input or a single filename argument (see the uniq man page for details) and, by default, removes any duplicates from the list.

If we want to see the list of duplicates instead, we add the “-d” option to uniq.

### wc - print the number of lines, words, and bytes 
***

Like our previous commands, if executed without command line arguments, wc accepts standard input. The “-l” option limits its output to only report lines. Adding it to a pipeline is a handy way to count things. 

### grep - find text patterns
***

`grep pattern [file...]`

When grep encounters a “pattern” in the file, it prints out the lines containing it.

There are a couple of handy options for grep: “-i” which causes grep to ignore case when performing the search (normally searches are case sensitive) and “-v” which tells grep to only print lines that do not match the pattern.

### head, tail - print the head or the tail of the file
***

Sometimes you don’t want all of the output from a command. You may only want the first few lines or the last few lines. The head command prints the first ten lines of a file and the tail command prints the last ten lines. By default, both commands print ten lines of text, but this can be adjusted with the “-n” option.

`head -n [numbers of line you wanna print] [file...]`

tail has an option which allows you to view files in real-time. This is useful for watching the progress of log files as they are being written. In the following example, we will look at the messages file in /var/log. Superuser privileges are required to do this on some Linux distributions, since the /var/log/messages file may contain security information.

Using the “-f” option, tail continues to monitor the file and when new lines are appended, they immediately appear on the display. This continues until you type Ctrl-c.

### tee - get the transport from stderr to stdout and file 
***

In keeping with our plumbing metaphor, Linux provides a command called tee which creates a “tee” fitting on our pipe. The tee program reads standard input and copies it to both standard output (allowing the data to continue down the pipeline) and to one or more files. This is useful for capturing a pipeline’s contents at an intermediate stage of processing.

### Useful Toturial
***

[catonmat](https://catonmat.net/bash-one-liners-explained-part-three)

## Staring at the world from Shell 
***

### (Character)Expansion
***

With expansion, youo type something and it is expanded into something ele before shell acts upon it.

echo is a shell builtin that performs a very simple task. It prints out its text arguments on stout.

`echo [content]`

However, if your input some wildcard for its arguments, the shell will expands the wildcard into something else. When the enter key is pressed, the shell automatically expands any qualifying characters on the command line before the command is carried out, so the echo only saw the expanded result. 

### Pathname Expansion
***

`echo [regular expression]`

If we wanna show the hidden files of the current directory, `echo .*` will also dispaly "." & ".." for us. To avoid this result, correct command is this `echo .[!.]?*` or `ls -d .[!.]?*`

### ~ - the tilde expansion
***

When used at the beginning of the word, it expands into the name of the home directory of the name user, or if no user is named, the home directory of the current user.

### Arithmetic expansion
***

Shell allow us to use the shell prompt as a calculator.

`echo $((expression))`

Where expression is an arithmetic expression consisting of values and arithmetic operators.

Arithmetic expansion only support integers, but can perform quite a number of different operations. Here are a few of the supported operators.

Space are not significant in arithmetic expressions and expressions may be nested. 

### Brace Expansion
***

With it, you can create multiple text strings from a pattern containing braces. Patterns to be brace expanded may contain a leading portion called a preamble and a trailing portion called a postscript.  The pattern may not contain embedded whitespace.

Here is an example using a range of integers:
`echo Number_{1..5}`. And the output is `Number_1  Number_2  Number_3  Number_4  Number_5`. 

Another example:
`echo {Z..A}`

And nexted:
` echo a{A{1,2},B{3,4}}b`

### Parameter Expansion
***

It’s a feature that is more useful in shell scripts than directly on the command line. Many of its capabilities have to do with the system’s ability to store small chunks of data and to give each chunk a name. Many such chunks, more properly called variables, are available for your examination.  With parameter expansion, if you misspell the name of a variable, the expansion will still take place, but will result in an empty string.

### Command Substitions
***

Command substitution allows us to use the output of a command as an expansion:
`echo $(ls)`. And this will print out the files'names which are in the current directory.

We are not limited to just simple commands. Entire pipelines can be used (only partial output shown):
`file $(ls /usr/bin/* | grep zip)`

### Double Quotes
***

If you place text inside double quotes, all the special characters used by the shell lose their special meaning and are treated as ordinary characters. The exceptions are $, \ (backslash), and ` (back-quote). This means that word-splitting, pathname expansion, tilde expansion, and brace expansion are suppressed, but parameter expansion, arithmetic expansion, and command substitution are still carried out. Using double quotes, we can cope with filenames containing embedded spaces.

By default, word-splitting looks for the presence of spaces, tabs, and newlines (linefeed characters) and treats them as delimiters between words. This means that unquoted spaces, tabs, and newlines are not considered to be part of the text. They only serve as separators. Since they separate the words into different arguments, our example command line contains a command followed by four distinct arguments. 

```
$ echo $(cal)
February 2008 Su Mo Tu We Th Fr Sa 1 2 3 4 5 6 7 8 9 10 11 12 13 14
15 16 17 18 19 20 21 22 23 24 25 26 27 28 29
$ echo "$(cal)"
February 2008
....

```

In the first instance, the unquoted command substitution resulted in a command line containing thirty-eight arguments. In the second, a command line with one argument that includes the embedded spaces and newlines.

### Single quotes
***

If we need to suppress all expansions, we use single quotes. 
```
$ echo text ~/*.txt {a,b} $(echo foo) $((2+2)) $USER
text /home/me/ls-output.txt a b foo 4 me
$ echo "text ~/*.txt {a,b} $(echo foo) $((2+2)) $USER"
text ~/*.txt   {a,b} foo 4 me
$ echo 'text ~/*.txt {a,b} $(echo foo) $((2+2)) $USER'
text ~/*.txt  {a,b} $(echo foo) $((2+2)) $USER
```

### Escape Character
***

Sometimes we only want to quote a single character. To do this, we can precede a character with a backslash, which in this context is called the escape character.
`echo "The balance for user $USER is: \$5.00"` 

And '$' will just be thought as a character.

It is also common to use escaping to eliminate the special meaning of a character in a filename. For example, it is possible to use characters in filenames that normally have special meaning to the shell. These would include “$”, “!”, “&”, “ “, and others.
`mv bad\&filename good_filename`

Always remember, to allow a backslash character to appear, escape it by typing “\”. Note that within single quotes, the backslash loses its special meaning and is treated as an ordinary character.

## Advanced Skills Of Keyboard Operating
***

bash uses a library (a shared collection of routines that different programs can use) called Readline to implement command line editing.

### Move The Cursor
***

| Key | Action |
|---|---|
| Ctrl-a | Move cursor to the beginning of the line. |
| Ctrl-e | Move cursor to the end of the line. |
| Ctrl-f | Move cursor forward one character;same as the right arrow key. |
| Ctrl-b | Move cursor backward one character;same as the left arrow key. |
| Alt-f | Move cursor forward one word. |
| Alt-b | Move cursor backward one word. |
| Ctrl-l | Clear the screen and move the cursor to the top left corner. The clear command does the same thing. |

### Edit Text
***

| Key | Action |
|---|---|
| Ctrl-d | Delete the character at the cursor location. |
| Ctrl-t | Transpose(exchange)the character at the cursor location with the one preceding it. |
| Alt-t | Transpose the word at the cursor location with the one preceding it. | Alt-l | Convert the characters from the cursor location to the end of the word to lowercase. |
| Alt-u | Convert the characters from the cursor location to the end of the word to uppercase. |





.... Needed to be completed



## Rights
***

### Owner, Group Member 
****

In the Unix security model, a user may own files and directories. When a user owns a file or directory, the user has control over its access. Users can, in turn, belong to a group consisting of one or more users who are given access to files and directories by their owners. In addition to granting access to a group, an owner may also grant some set of access rights to everybody, which in Unix terms is referred to as the world. To find out information about your identity, use the id command.
`id` and its result `uid= gid= groups=`

When user accounts are created, users are assigned a number called a user ID or uid which is then, for the sake of the humans, mapped to a user name. The user is assigned a primary group ID or gid and may belong to additional groups.

Fedora starts its numbering of regular user accounts at 500, while Ubuntu starts at 1000. We can see that the Ubuntu user belongs to a lot more groups.

User accounts are defined in the /etc/passwd file and groups are defined in the /etc/group file. When user accounts and groups are created, these files are modified along with /etc/shadow which holds information about the user’s password. For each user account, the /etc/passwd file defines the user (login) name, uid, gid, the account’s real name, home directory, and login shell. If you examine the contents of /etc/passwd and /etc/group, you will notice that besides the regular user accounts, there are accounts for the superuser (uid 0) and various other system users.

###  Read Access, Write Access, and Execution Access
***

When we use `ls -l` command, we can see some symbol in the front of the result. Let's try to understand these symbol. The first ten characters of the listing are the file attributes. The first of these characters is the file type:
| Attribute | File Type |
|---|---|
| - | a regular file |
| d | A directory |
| l | A symbolic link. Notice that with symbolic links, the remainning file attributes are always “rwxrwxrwx” and are dummy values. The real file attributes are those of the file the symbolic link points to. |
| c | A character special file. This file type refers to a device that handles data as a stream of bytes, such as a terminal or modem. |
| b | A block special file. This file type refers to a device that handles data in blocks, such as a hard drive or CD-ROM drive. |

The remaining nine characters of the file attributes, called the file mode, represent the read, write, and execute permissions for the file’s owner, the file’s group owner, and everybody else.

When set, the r, w, and x mode attributes have the following effect on files and directories:
| Attribute | Files | Directories |
|---|---|---|
| r | Allows a file to be opened and read. | Allows a directory's contents to be listed if the execute attribute is also set. |
| w | Allows a file to be written to or truncated, however this attribute does not allow files to be renamed or deleted. The ability to delete or rename files is determined by directory attributes. | Allows files within a directory to be created, deleted, and renamed if the execute attribute is also set. |
| x | Allows a file to be treated as a program and executed. Program files written in scripting languages must also be set as readable to be executed. | Allows a directory to be entered, e.g., cd directory. |

### chmod- Change The Mode Of A File
***

Be aware that only the file’s owner or the superuser can change the mode of a file or directory. chmod supports two distinct ways of specifying mode changes: octal number representation, or symbolic representation. 

With octal notation we use octal numbers to set the pattern of desired permissions. Since each digit in an octal number represents three binary digits, this maps nicely to the scheme used to store the file mode(Comprehend these with converting it to binary). We use three octal as arguments to set the access to the the file’s owner, the file’s group owner, and everybody else.

| Octal | File Mode |
|---|---|
| 0 | --- |
| 1 | --x |
| 2 | -w- | 
| 3 | -wx |
| 4 | r-- |
| 5 | r-x | 
| 6 | rw- |
| 7 | rwx |

chmod also supports a symbolic notation for specifying file modes. Symbolic notation is divided into three parts: who the change will affect, which operation will be performed, and what permission will be set. To specify who is affected, a combination of the characters “u”, “g”, “o”, and “a” is used as follows:

|---|---|
| u | Short for "user", but means the file or directory owner. |
| g | Group owner. |
| o | Short for "others", but means world. |
| a | Short for "all", the combination of "u", "g", and "o". |

If no character is specified, “all” will be assumed. The operation may be a “+” indicating that a permission is to be added, a “-” indicating that a permission is to be taken away, or a “=” indicating that only the specified permissions are to be applied and that all others are to be removed.

example
`chmod a+rw`


### umask- Set The Default Access Permission
***

To understand the *umask* command, we need to convert octal number to binary number and translate it to the mode of the file. Then the argument you add after umask is to do an *xor* operation on the default mode. 

