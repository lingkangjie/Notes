# basic commands
- $ date, cal(calender), df (current amount of free space on disk driver), free (free memory)
- ls, -l use a long listing format, -t sort the result by file's modification time, --reverse -r reverse the results, -S sort results by file size, -h human readable.
- $ file, determining the file's type. $ less, viewing the file contents with less.
- $ cp, -i --interactive prompt before overwrite, -r --recursive, -u --update copy only when the SOURCE file is newer than the distination file or when the destination file sis missing. -v --verbose, display copy information.
- $mv file1 file2 dir1 move file1 and file2 to dir1.
- $rm -i --interactive, -v --verbose, usage just like above.
- change stander output using >, such as $ls -l > tmp.txt. Using >> to append new output, such as $ls -l /usr/bin >> tmp.txt.
- redirecting standard error to a file: 
```
$ ls -l /bin/usr 2> ls-error.txt
```
When `$ less ls-error.txt`, ouput `ls: cannot access '/bin/usr': No such file or directory`.
Here file discriptor, 1, 2, 3 is represented standard input, standard ouput, standard error, respectively. The descriptor 2 is placed immediately befor the redirection operator >.

- redirecting standard input and standard error to one file. Append method: `$ls -l /bin/usr >> ls-error.txt 2>&1`. First, we redirect standard output to file ls-error.txt and then we redirect file descriptor 2 (standard error) to file descriptor 1 (standard output) using the notation 2>&1. Notice that the order of the redirections is significant. The redirection of standard error must occur *after* redirecting output or it does not work.

- Using `&>` to redirect both standard output and standard error to file. `$ls -l /bin/usr &>> ls-error.txt`.

- $cat, changing the standard input. Display file: $cat filename. Concatenate files together: $cat file1 file2 > merged-files. Read inputs from standard Input IO to files: $cat > tmp.txt (use ctrl + d to tell *cat* that it has reached end of file (EOF).

- Pipelines. The difference between > and |: one connects a command with file with file, other connects a command with a command, command1 > file1, command1 | command2.

- `$ls /bin /usr/bin | sort | uniq -d | less`, use uniq to remove any duplicates from the output of sort command, use -d to see the list of duplicates instead.

- wc, word count, used to display the number of lines, words, and bytes contained in files, -l limits its output to only report lines.`$ls /bin /usr/bin | sort | uniq | wc -l`
- grep, print lines matching a pattern. grep pattern [file...].
- tail, head, print end/first part of files, such as head -n 10, prints first 10 lines.
- tee, read from standard input and write to standard output and files, it is useful for capturing a pipeline' contents at an intermediate stage of processing, `$ls /usr/bin | tee ls.txt | grep zip`, capture the standard output of ls to ls.txt before grep filters the pipeline's contents.
- Brace expansion: 
```
lkj@lkj:~/tmp/Notes$ echo N_{001..11}
N_001 N_002 N_003 N_004 N_005 N_006 N_007 N_008 N_009 N_010 N_011
lkj@lkj:~/tmp/Notes$ echo {Z..A}
Z Y X W V U T S R Q P O N M L K J I H G F E D C B A
lkj@lkj:~/tmp/Notes$ echo a{A{1,2},B{3,4}}b
aA1b aA2b aB3b aB4b
```
- Command Substitution, allows us to use the output of a command as an expansion. `$ file $(ls -d /usr/bin/* | grep zip)`, means after *grep* filters, *file* the results.
- Move cursor around, as I use tmux and xshell at the same time, I find that `ctrl +a`(move cursor to the beginning of the line), `ctrl+e` (move the cursor to end end of the line), `ctrl + k`(kill text from the cursor location to the end of line), `ctrl+u`(kill text from the cursor location to the beginning of the line), `ctrl+f` (the same as right arrow key), `ctrl+b` (conflicts with tmux ctrl+b, but still works alternately)  work.
- History. Search history: $history | grep /usr/bin. When we get the line number of the command in the history list, we can execute it by `!number`, e.g. `!80`. Search history in reverse: first `ctrl+r` to enter the reverse search env, then type the contents you want to search, such `/usr/bin`, use `ctrl+j` to copy the command to our current command line for futher editing or execute. `ctrl+p`, move to previous history entry. `ctrl+n`, move the next history entry. `!!` repeat the last command.
- file property.
```
drwxr-xr-x 12 lkj lkj    4096 May 26 18:21 ..
-rw-rw-r--  1 lkj lkj       0 May 26 19:15 foo.txt
```
\- : a regular file, d : directory, l : symbolic link, and the remaining file attributes are always "rwxrwxrwx", c : character file, b : block special file.

"rwx(Owner) rwx(group) rwx(world, everybody else)", `r` allows file to be opened and read, `w` allows to written to or truncated, `x` allows to be treated as a program and executed.
- chmod, change file mode, e.g., `$chmod 600 foo.txt`, `$chmod 777 foo.txt`. Another way, u, g, o, a represent short for user, short for owner, short for others or world or everybody else, short for all. +, - represent add, minus attributes. r, w, x represent attributes. e.g., `u+x` add execute permission for the owner, `u-x` remove execute permission from the owner, `+x` as the same as `a+x` add execute permission for owner, group, world.
- chown, change file owner and grop. chgrp, change group ownership. passwd [user], change your password.
- By default, `ps` only show the processes associated with the current terminal seesion, tty(short for teletype, refers to controlling terminal). `ps x` will show all processes.
- top
```
top - 19:47:36 up  1:27,  4 users,  load average: 0.07, 0.09, 0.09
Tasks: 317 total,   1 running, 226 sleeping,   0 stopped,   0 zombie
%Cpu(s):  0.5 us,  0.8 sy,  0.0 ni, 98.1 id,  0.5 wa,  0.0 hi,  0.0 si,  0.0 st
```
`top` the name of the program. `up 1:27` the machine was running 1 hour and 27 minutes. `load avergae`, the number of processes that are in a runnable state and are sharing the CPU, the first is average for last 60 seconds, next is previous 5 minutes, next is previous 15 minutes, values less than 1.0 indicate that the machine is not busy. `0.5 us` 0.5% of CPU is being used for **user processes**, `0.8 sy` 0.8% of CPU is being used for **system(kernel)** processes, `0.0 ni` 0.0% of CPU is being used by "nice"(low-priority) processes. `98.3 id` 98.3% of CPU is idle. `0.5 wa` 0.5% of CPU is waiting for I/O.
- The most importance startup file `~/.bashrc` for Non-Login Shell Session, it is always read.
- export, set export attribute for shell variables, that is to say update $Variable. e.g. `$ PATH=$PATH:$HOME/bin`, and then update $PATH by `export PATH`.
```
lkj@lkj:~/tmp/Notes$ foo="ok"
lkj@lkj:~/tmp/Notes$ foo=$foo:$HOME/data
lkj@lkj:~/tmp/Notes$ echo $foo
ok:/home/lkj/data
```
- Which files should we modify for establishing environment? To add directories to your *PATH* of define additional environment variables, place those changes in **.bash_profile**( or **.profile** in Ubuntu). For everything else, place the changes in **.bashrc**.
- In Nano editor, ^ means Ctrl, such as, ^X means Ctrl-x.

# wildcard
- \* matches any characters
- ? matches any single character
- [characters] matches any character that is member of the set **characters**
- [!characters] 
- [[:class:]] matches any character that is a member of specifiled class.
- [:alnum:] matches any alphanumeric character. [:alpha:] matches any alphabetic character. [:digit:] matches any numeral. [:lower:] lowercase. [:upper:] uppercase.
- [[:upper:]]\* any file beginning with an uppercase letter.
- \*[[:lower:]123] any file ending with lowercase letter or the numerals 1 2 3.
