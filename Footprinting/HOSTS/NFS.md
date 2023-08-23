```bash
# Nmap scan
nmap 10.129.14.128 -p111,2049 -sV -sC

# Use nmap scripts
nmap --script nfs* 10.129.14.128 -sV -p111,2049

# Show Available NFS Shares
showmount -e 10.129.14.128

# Mounting NFS Share
mkdir target-NFS
mount -t nfs 10.129.14.128:/ ./target-NFS/ -o nolock

# List Contents with Usernames & Group Names
ls -l mnt/nfs/

# List contents with UID/GUID
ls -n mnt/nfs/

# unmountung
umount ./target-NFS
```
