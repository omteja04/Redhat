<!--
  Author: omteja04
  Created on: 09-06-2024 06:04:27
  Description: Find
-->
<!-- cSpell:disable
 -->

```sh
# Create directories for the example
mkdir -p /example_dir/sarah_files
mkdir -p /example_dir/other_files

# Create files owned by 'sarah'
touch /example_dir/sarah_files/file1.txt
touch /example_dir/sarah_files/file2.log
chown sarah:sarah /example_dir/sarah_files/file1.txt
chown sarah:sarah /example_dir/sarah_files/file2.log

# Create files owned by other users
touch /example_dir/other_files/file3.txt
touch /example_dir/other_files/file4.log
chown root:root /example_dir/other_files/file3.txt
chown root:root /example_dir/other_files/file4.log
```

```sh
mkdir /root/find.user
```

This command creates a new directory named `find.user` in the `/root` directory. The `mkdir` command stands for "make directory."

```sh
find / -user sarah -type f -exec cp {} /root/find.user/ \;
```

This command uses the `find` utility to search for files. Here's a breakdown of the options used:

- `/` : This specifies the starting directory for the search, which is the root directory.
- `-user sarah` : This option tells `find` to search for files that are owned by the user `sarah`.
- `-type f` : This option tells `find` to search for objects of type "file" (as opposed to directories or other types of objects).

- `-exec` : This option is followed by the command to execute (`cp`) and a set of curly braces `{}`. The `{}` will be replaced by the current file path found by `find`.
- `cp {}` : This part specifies the command to be executed, which is `cp` (copy). It will copy each file found to the specified directory.
- `/root/find.user/` : This is the target directory where the files will be copied.
- `\;` : This terminates the `-exec` command.

```
ls -a /root/find.user
```

This command lists all files and directories in the `/root/find.user` directory, including hidden files (those starting with a dot `.`), as specified by the `-a` option.
