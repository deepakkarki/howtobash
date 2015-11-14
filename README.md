# How to Bash
This repository is a collection of frequent **"How to's"** that command line newbies face. I'm creating this repository for personal reference, and for those who plan to get more comfortable with the Linux development environment. 

Most of the content will be of the format "How to ..." (eg. How do I automate my ssh scripts) and "How do I ..." (eg. check the memory being used by each process).

##Why

There are quite a few reasons behind this initiative, to break it down :

**Why deal with bash?** 

Programming and development are two different things. To be a better developer I need to know my tools better - they don't teach this at college. 

**Why not use reference books?** 

Current resources teach you topic by topic, many reference books and bibles available. I get bored reading before I get something meaningful. Here I introduce commands in context to problems, not the other way round. Once you have the hang of the basics, you'll know what to search for in the man pages / reference books.

**Why put it on Github?** 

There is a need for a community driven resource as such. Stackoverflow will help when you know the exact question to ask, here you will probably find solutions to questions you wouldn't think of asking. (Like when my friend introduced me to tmux a while back - such a life saver!)

##Note

**This will be beneficial to you if**

1. You already have some basic programming and scripting experience
2. Use linux - but are still primarily dependent on the desktop GUI to get your work done.
3. Understand that this is just to help you start, and not a replacement to indepth reference materials.


```
```

##0. Understanding the terminal and shell
(understand shell vs terminal, the different kinds of terminal - longin, non login, etc)

##1. Shell settings
(bash_profile, bashrc, PS, etc)

##2. Bash redirects

###A. Redirect output

* **stdout** : 
This is used to redirect an output to file.
```sh
$ echo hello > greetings 
$ cat greetings 
hello
```
* **stderr** : 
Redirect the error messages to a file
```sh
$ cat noFile 2> err.log
$ cat err.log 
cat: noFile: No such file or directory
```
* **All output** : 
This includes both stdout and stderr
```sh
$ cmd &> allLog.txt
# To send output to one file and err to another - 
$ cmd > log.out 2> log.err
```
* **Append to file** : 
Echo creates a new file everytime, to append use the `>>` operator.
```sh
$ echo first > msg.txt
$ echo second >> msg.txt
$ cat msg.txt 
first
second
```
* **Group redirection** : 
A common redirection for a set of commands 
```sh
$ { echo hello; echo world; } > msg.txt 
$ cat msg.txt 
hello
world
```

###B. Redirect input

* **Read from file** : 
Get the stdin from a file instead of terminal.
```sh
$ cat < msg.txt
hello
world
```
* **Here file** : 
Type in lines until the said literal, in this case `EOL`. The lines typed in are fed as stdin.
```sh
cmd << EOL 
line1 
line2 
EOL 
```

* **Anon FIFO** : 
When we don't want to manipulate stdin of a file, we use this method. 
```sh
$ cat <( echo hello ) 
hello
```
Here a new anonymous FIFO is created, `echo` output is redirected there. The FIFO path is passed as a parameter to `cat`.
The FIFO path looks something like `/dev/fd/63`, `cat` opens and reads it.

###C. Process pipes

* **Simple piping** : 
Here we pipe one process's output (stdout) to another process's input (stdin)
```sh
$ history | grep "cat" | tail -5
 1154  cat < msg.txt 
 1155  cat <( echo x ) 
 1156  cat <( echo hello ) 
 1159  history | grep "cat"
 1161  history | grep "cat" | tail -5
```
There are three commands here. `history` lists all the previous commands made, that output is sent to `grep` which selects the commands with "cat" in them. This output is sent to `tail` which prints the last five lines. So this `history | grep "cat" | tail -5` gives us the 5 latest commands that had the word "cat" in them.

* **stdin and stderr** : 
Piping can redirect both stdout and stderr of one process to stdin of another.
```sh
$ cmd |& cmd2
```

* **xargs** : 
Sometimes we need to supply the output of one program as an argument to the next. This is when the second program reads the data as a command line argument and not from the stdin.
```sh
$ echo greetings | xargs cat
hello
```
Here xargs reads the output of `echo` from it's stdin. Then executes the `cat` command with "greetings" as the parameter. Another way to do this would be 
```sh
$ cat $( echo greetings )
hello
```

##3. Programming in Bash

##4. Files 

##5. Processes 

##6. Hardware
(wonder if I should have different sub headings for processor, network card, hard disks, RAM, etc)

##7. Network 

##8. System
(managing the system preferences, access control, etc)

##9. General utilities 
(search, replace, automate simple stuff etc.)

##10. Remote
(ssh, scp, etc)
