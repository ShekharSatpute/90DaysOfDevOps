# Day 10: File Permissions & File Operations Challenge

## Files Created

Created and verified files using:

```
touch devops.txt
echo "DevOps practice" > notes.txt
touch script.sh
ls -l
```

![create files](images/1%20create%20files.png)

---

## Read Files

- Read notes.txt 

```
cat notes.txt
```

![notes](images/2%20notes.png)

- Display first 5 lines of /etc/passwd:

```
head -n 5 /etc/passwd
```

![head](images/3%20head.png)

- Display last 5 lines:

```
tail -n 5 /etc/passwd
```

![tail](images/4%20tail.png)

---

# Permission Changes

## Understand Permissions

![permissions](images/5%20permissions.png)

### Current permissions :

Devops.txt : `-rw-rw-r--`

- `-` → Regular file
-  `rw-` → Owner: read + write
- `rw-` → Group: read + write
- `r--` → Others: read only

The same permissions were applied to notes.txt and script.sh.

---

## Modify Permissions

- Make script.sh executable → run it:

```
chmod +x script.sh
./script.sh
```

![run script](images/6%20run%20script.png)

- Make devops.txt read-only:

```
chmod -w devops.txt
```

![read only](images/7%20read%20only.png)

- Set notes.txt to 640:

```
chmod 640 notes.txt
```

- Owner → rw-
- Group → r--
- Others → ---

![notes permission](images/8%20notes%20permission.png)


- Create directory project/ with permissions 755

``` 
mkdir -m 755 project 
```

![project](images/9%20project.png)


---

# Test Permissions

**Write to a read-only file**

```
echo "test" >> devops.txt
```
**Result:** Permission denied because write permission was removed.

![readonly](images/10%20readonly.png)

---

**Execute without execute permission**

```
./script.sh
```

**Result:** Permission denied because the file does not have execute permission.

After adding execute permission:
```
chmod +x script.sh
./script.sh
```
The script runs successfully.

![test](images/11%20test%20.png)

---

# Commands Used

- `touch filename` - Creates an empty file.
- `echo "Hello" > filename` - Create file with content.
- `cat filename` - Read file content.
- `vim filename` - Create/open file in Vim.
- `vim -R filename` - Open file in read only mode.
- `head -n 5 /etc/passwd` - Show first 5 lines.
- `tail -n 5 /etc/passwd` - Show last 5 lines.
- `chmod +x filename` - Adding executable permission.
- `chmod -w filename` - Removing write permission.
- `chmod 640 filename` - Set numeric permissions
- `mkdir -m 755 dname` - Create directory with permissions.
- `ls -l` - View file permissions.


# What I Learned

- Linux permissions control access to files and directories.
- Execute permission is required to run shell scripts.
- Removing write permission prevents file modification.
- chmod supports symbolic and numeric modes.
- File and directory permissions control access differently.
