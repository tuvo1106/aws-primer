# Linux Foundation Certified SysAdmin (LFCS)

## Essential Commands

### Searching for files

**Basic Searching**

```sh
# Search in root directory
find / -name "test.txt"
# Case insensitive searches
find /etc -iname "text.txt"
# Find opposite of
find /etc -not -name "text.txt"
```

**See volumes**

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

**Types**

```sh
# Find symbolic links
find / -type l
# Find directories
find / -type d
# Find all files that end with log
find / -type f -name "*.log"
```

**Other Flags**

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

**Chain Commands**

```sh
# Change permissions
find / -name "test.txt" -exec chmod 700 {} \;
```

**Locate**

```sh
# Needs local database
locate test.txt
```

---

### Evaluate and Compare the Basic File System Features and Options

**What is a Filesystem?**

- A block device is a set of addressable blocks used to store and retrieve data:
  - magnetic hard drive
  - ssd
  - usb flash storage
- A filesystem is where a computer persists general data for users and/or applications
- Filesystems can affect:
  - performance of the system
  - Efficiency of the media
  - Compatibility with other systems

**What is Journaling**

- Designed to prevent data corruption from crashes or power loss
- Adds a bit of overhead to file writes
- Some high-performance servers might not necessarily need it
- Often not used on removable media such as removable flash drives

**Ext, Ext2, Ext3, Ext4**

- ext - "extended file system"
- ext2 - first file system to support extended file attributes (x-attrs) and 2TB+ drives
- ext3 - introduced journaling
- ext4 - designed to be backward compatible and introduced some additional features

**BtrFS**

- B-Tree File System
- Drive pooling, snapshots, compression, online defragmentation

**ReiserFS**

- Lots of new features such as special efficiencies for small text files
- Designed by Hans Reiser
- Unlikely to continue development

**ZFS**

- Designed by Sun Microsystems (acquired by Oracle)
- Drive pooling, snapsots, dynamic disk striping
  - all features BtrFS bring to Linux when it's the default system
- Each file has a checksum
- Open-sourced under Sun CDDL license
- Installing ZFS is fairly easy on any linux dist
- Ubuntu offers official ZFS support starting with 16.04
  - Uses it for containers by default

**XFS**

- Ported to Linux in 2001
- Similar to Ext4
- Can be enlarged (but not shrunk) on the fly
- Good with large files (like backup servers)
- Poor with many small files (like serb servers)

**JFS**

- Journaled File System
- Developed by IBM
- Low CPU usage
- Good performance regardless of file server
- Partitions can by dynamically enlarged but not shrunk
- Support in most every major dist
- Not as widely tested in production as Ext4

**Swap**

- Not used as an actual file system -- virtual memory
- Scratch space for stuff that won't fit in RAM
- Hibernating
- Analogous to Windows Paging File

**FAT (FAT16, FAT32, exFAT)**

- Microsoft's "File Allocation Table" file system
- NOT JOURNALED
- Great for USB drives that you'll be using on Windows or Apple hardware

---

### Compare and Manipulate File Content and Use Input-Output Redirection

**Sort**

```sh
sort shoppinglist.txt | more
# Reverse
sort -r shoppinglist.txt | more
```

**Redirection**

```sh
cat hardwarelist.txt shoppinglist.txt | sort > combined.txt
```

**Format**

```sh
# Cleans up whitespace
fmt -u format.txt
```

**Count number of lines**

```sh
nl combined.txt
```

**Remove delimiters**

```sh
cut -d ";" -f1 delimited.txt
```

---

### Analyze Text Using Basic Regular Expressions

```sh
# Match every line that starts with 'the'
grep '^the' alice.txt
grep '^T[a-z][aeiou] ' alice.txt

# Third char not 'e'
grep '^Th[^e]' alice.txt

# + is 1 or more, * is 0 or more
grep '^T[h+]' alice.txt

# Find every instance of 'the'
grep '\<[tT]he\>' alice.txt

# Find any two same lowercase letters (back-reference)
grep '\([a-z]\)\1' alice.txt
```

---

### Archive, Backup, Compreses, Unpack, and Decompress Files

**Tar (tape archive)**

```sh
# No compression, c: create, v: verbose, f:file
tar cvf databackup.tar /data

# List tarball contents
tar tvf databackup.tar
```

**Zip**

```sh
gzip databackup.tar

# Tar and zip
tar cfvz databackup.tar.gz /data

# Extract
tar xfvz databackup.tar.gz
```

---

### Create and Manage Hard and Soft Links

- hard links point to the direct inodes on disk where the file lives
- name does not matter
- changing content of hard link will change all refs
- deleting hard link will still presist original until all references are gone

```sh
# Hard link
ln <to> hardlink
```

- soft links point anywhere you can specify a file, e.g. different file systems
- if you delete original sym link, the link is broken

```sh
# Soft link
ln -s <to> softlink
```

---

## Operation of Running Systems

### Boot, reboot, and shut down a system safely

```sh
# Correct way to reboot Linux machine
sudo shutdown -r now
sudo reboot # same command

# See active users
w
```

### Boot or change system into different operating modes

- System V Runlevels

```
# See what runlevel
runlevel
# Runlevel 0
sudo shutdown -h
# Runlevel 6
sudo reboot
```
