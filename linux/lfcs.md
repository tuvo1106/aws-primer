# Linux Foundation Certified SysAdmin (LFCS)

### Searching for files

##### Basic Searching

```sh
# Search in root directory
find / -name "test.txt"
# Case insensitive searches
find /etc -iname "text.txt"
# Find opposite of
find /etc -not -name "text.txt"
```

##### See volumes

```sh
# -h: human readable
df -h
```

```
Filesystem      Size   Used  Avail Capacity iused      ifree %iused  Mounted on
/dev/disk1s1   233Gi   10Gi  195Gi     6%  487584 2447613736    0%   /
devfs          200Ki  200Ki    0Bi   100%     709          0  100%   /dev
/dev/disk1s2   233Gi   24Gi  195Gi    12%  544547 2447556773    0%   /System/Volumes/Data
/dev/disk1s5   233Gi  3.0Gi  195Gi     2%       3 2448101317    0%   /private/var/vm
map auto_home    0Bi    0Bi    0Bi   100%       0          0  100%   /System/Volumes/Data/home
```

##### Types

```sh
# Find symbolic links
find / -type l
# Find directories
find / -type d
# Find all files that end with log
find / -type f -name "*.log"
```

##### Other Flags

```sh
# Find anything larger than 27000 bytes
find /usr/bin -size +27000c
# Find by time created
find / -type f -mtime 1
# Find file by owned user
find / -user user
# Find by permission
find /usr/bin -perm 755
```

##### Chain Commands

```sh
# Change permissions
find / -name "test.txt" -exec chmod 700 {} \;
```

##### Locate

```sh
# Needs local database
locate test.txt
```

---

### Evaluate and Compare the Basic File System Features and Options
