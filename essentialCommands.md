1. ssh mohit@192.168.13.12 -> ssh command, name we would like to use in remote machine, ip of remote machine
2. --help -> to know about the command and also options available with the command
3. man pages
4. `use --help` -> when you forgot command line options. `use man` -> dive deep
5. `apropo` -> search through man pages. apropos relies on a database, a program must refresh it periodically.
6. apropo -s 1 director -> will only give command with man page of section 1
7. `mandb` -> manually refresh man pages
8. on VMs database is not created , se we run `sudo mandb`
9. system calls provided by linux kernel `????`
10. when we want to make our searches open and match more stuff use generic name with `apropos` command
11. `systemctl press tab twice` -> it will give `options` `for` that `command`. But in this it is not necessary that all the options are included in the suggestion list
12. press `tab after command`, if command interpreter figures out that it will give command, if it cannot figure out then press `tab twice` it will give all the suggestions.
13. tab once for autocompletion and it also supports mini commands. Tab twice to see more than one suggestions of commands or options or autocomplete options
14. Tab suggestions and autocompletions also work for files and directories names eg: `ls /u then press tab if one suggestion got figured out by interpreter then it will show if more than one suggestions then press tab twice`
15. `manuals`, `--help`
16. so take a command we know nothing about and read with man or --help to do something with it. It will practise us for looking for help quickly
17. `hostnamectl`
18. `ssh` -> ssh other_host | then fingerprint confirmation | then other host's password | then you are logged in to other host | then write `exit` now you will exit that host

`Configuration file, NFS mount` ->

-- apropos "NFS mounts"
-- nfsmount.conf (5) - Configuration file for NFS mounts
-- create file -> vi /home/bob/nfs and save name of configuration file for NFS mounts

19. ls -l -> to show files and directories in long list format. We can also combine two command line options and in that case order does not matter and there is also no need to put dash in front of each of them. One dash in the starting will suffice
20. `-h option` -> display file sizes in human readable format. Often used with -l(long list option for ls). This will list the contents of a directory and display the sizes of the files
21. `linux file system` -> hierarchical structure of the files and directories
22. every user starts in its home directory(/home/mohit)
23. root or superuser or administrator starts in root directory(/)
24. `absolute path` starts with root directory
25. `relative paths` gets added to the current directory
26. `cd /` -> to root directory. `cd -` -> go to previous directory. `cd` -> to home direc
27. all the commands accept both relative and absolte path
28. it is a good practise to end your directories with `slash /`. So in future we can differentiate, between file and direc
29. to copy directories -> `cd -r source destination`. `-r` -> command line `option/flag`
30. `while copying directories, the target directory name should be unique, if we specify name that already exists then the copied directory would end up in Documents folder ????` -> Essential commands/create-delete-copy-move file and direc/topic inside video `copying directories`
31. rename a file or directory -> `mv`. To rename a directory we can use new name as destination. We don't need to use -r flag with `mv`, `mv` takes care of all of that itself. Moving directories from one location to another location will also not require `-r flag`
32. When `copy or delete directories`, use -r flag

## Hard links ->

-- echo "some text" > filename -> creates a file and adds this text in it
-- `stat` command -> info about files and direc
-- files systems like XFS, ext4 etc keep track of data with the help of `inodes`
-- `inodes` -> keep track of file, data, metadata. Files points to inodes and inodes point to all data we require
-- `hard link` -> file to inode
-- `stat` command will show the number of hardlinks from file to inode
-- copying will create duplicate data.
-- create hard link -> `ln path_to_target path_to_linkfile`. Link file is the name of the new hard link we create
-- hardlink created at the destination is a file like anyother. But it points to the same inode as target file
-- If we delete a file with hardlink in one location, then the other location is not affected by this because the `inode` will still have one `hardlink` to it.
-- when there are zero hardlinks to inodes then the data will be erased from the disk
-- we can only `hardlinks to files and not directories`
-- only `hardlinks to files on same file system`. If we had an `external drive` mounted at `/mnt/backups` then we would not be able to hardlink a file from our SSD at /home/mohit to some other file on /mnt/backups since that is a diff file system
-- make sure we have the proper permission to create the link file at destination. So in our case we will need `write` permission
-- when we hardlink a file, make sure all users involved have the permission to access the file. So we will add users(username) to same group. Then we will use the command to allow group read and write to this file
-- We only need to change the permissions on one of the hard links, because we are changing permissions stored by the inode
-- so once we change permission of a file at one location, the other location hardlink will also have the same permission

useradd -a -G faimly mohit
useradd -a -G family swetank
chmod 660 index.html

## Soft links ->

-- file that points to the path. It is almost like a text file with the path to file or directory inside
-- create soft link with `-s or --symbolic option`
-- `ln -s path_target_file path_link-file`
-- to read the complete path the short link points to -> `readlink path_to_softlinkfile`
-- `ls -l ` will not show the complete path of original file
-- all the permission bits for the soft link file is `rwx -> read write execute`
-- permission of softlink does not matter, because if we write to a soft link file then the it will only write if there is write permission to the file that the soft link file is linking to. SO the `permission of destination file apply`
-- if we change one of the directory name in destination file path, then the `soft link will break`
-- We can see broken links highlighted in red in `ls -l` command. To tackle this we can create `soft link with relative path`. This way when we access soflink file they will get redirected to the destination file relative to the directory where soft link is
-- we can also `soft link to directory` like `ln -s pictures/ shotcut`
-- can also `soft link to files or directories on different file system`
-- `cp -a` -> to preserve the attributes while copying
-- `mkdir -p /tmp/1/2/3/4/5/6/7/8/9` -> to create the directory and its parent directory in one go
-- `ls --full-time` -> display the full/exact last modified time for the files
-- `uname` -> print system information
-- `lsb_release` - print distribution-specific information
