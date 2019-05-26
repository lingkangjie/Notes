# basic comands
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

# wildcard
- \* matches any characters
- ? matches any single character
- [characters] matches any character that is member of the set **characters**
- [!characters] 
- [[:class:]] matches any character that is a member of specifiled class.
- [:alnum:] matches any alphanumeric character. [:alpha:] matches any alphabetic character. [:digit:] matches any numeral. [:lower:] lowercase. [:upper:] uppercase.
- [[:upper:]]\* any file beginning with an uppercase letter.
- \*[[:lower:]123] any file ending with lowercase letter or the numerals 1 2 3.
