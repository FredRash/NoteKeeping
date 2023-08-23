For getting a shared file from the system we use mount.

For showing if there is a file to share -> showmount -e [ip]
For taking the file -> mount -t nfs [ip]:[the file to take] path to a directory