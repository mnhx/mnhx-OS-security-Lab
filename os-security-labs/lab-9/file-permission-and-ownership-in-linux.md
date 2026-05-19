# File Permission and Ownership in Linux

## Lab 9

## File Permission and Ownership in Linux

***

### Before You Start

Every file in Linux has an **owner**, a **group**, and **permissions** that control who can read, write, or execute it.

Useful commands to know who you are:

```bash
whoami      # shows your username
groups      # shows your groups
who         # shows who is logged in
```

***

### Permission Groups

Each file has 3 permission groups:

* **owner** → the user who owns the file
* **group** → users in the assigned group
* **others** → everyone else

<figure><img src="../../.gitbook/assets/image (204).png" alt=""><figcaption></figcaption></figure>

***

### Permission Types

Each group has 3 permission types:

| Symbol | Meaning       |
| ------ | ------------- |
| `r`    | Read          |
| `w`    | Write         |
| `x`    | Execute       |
| `-`    | No permission |

When you run `ls -l`, you see something like:

```
-rw-r--r--  1  kali  kali  0  May 18  testfile
```

The 9 characters after the first `-` or `d` are the permissions:

* First 3 → **owner**
* Middle 3 → **group**
* Last 3 → **others**

***

### Lab Exercise

#### Step 1 — Create a Directory and File

```bash
mkdir TEST
touch testfile
ls
```

<p align="center"><img src="../../.gitbook/assets/image (1).png" alt=""></p>

***

#### Step 2 — View Permissions

```bash
ls -lh
```

<p align="center"><img src="../../.gitbook/assets/image (2).png" alt=""></p>

> The first character tells you if it's a **directory (d)** or a **file (-)**.

***

#### Step 3 — Change Permissions with `chmod`

**Add execute for everyone:**

```bash
chmod +x testfile
ls -lh
```

<p align="center"><img src="../../.gitbook/assets/image (3).png" alt=""></p>

**Remove execute from everyone:**

```bash
chmod -x testfile
ls -lh
```

<p align="center"><img src="../../.gitbook/assets/image (4).png" alt=""></p>

**Add execute for owner only:**

```bash
chmod u+x testfile
```

**Add read+write for group:**

```bash
chmod g+rw testfile
```

**Add multiple permissions at once:**

```bash
chmod u+r,g+x testfile
```

> **Note — symbols:**
>
> * `u` → owner, `g` → group, `o` → others, `a` → all
> * `+` → add, `-` → remove

***

#### Step 4 — Set Permissions Using Numbers

Each permission maps to a number:

```
r = 4,  w = 2,  x = 1
```

Add them together: `rwx = 4+2+1 = 7`

```bash
# owner=rwx, group=r-x, others=---
chmod 740 testfile
ls -lh
```

<p align="center"><img src="../../.gitbook/assets/image (5).png" alt=""></p>

```bash
# Full permissions for everyone
chmod 777 testfile
ls -lh
```

<p align="center"><br><img src="../../.gitbook/assets/image (6).png" alt=""></p>

***

#### Step 5 — Copy Permissions from Another File

```bash
chmod --reference=testfile testfile2
ls -lh
```

<p align="center"><img src="../../.gitbook/assets/image (7).png" alt=""></p>

***

#### Step 6 — Apply Permissions Recursively

```bash
chmod -R g+r TEST 
ls -lh
```

<p align="center"><img src="../../.gitbook/assets/image (8).png" alt=""></p>

***

#### Step 7 — Change Ownership with `chown`

First, add a new user:

```bash
sudo adduser ahmed
```

<p align="center"><img src="../../.gitbook/assets/image (9).png" alt=""></p>

Now change the owner of a file:

```bash
sudo chown ahmed file1.txt
ls -l file1.txt
```

<p align="center"><img src="../../.gitbook/assets/image (10).png" alt=""></p>

> **Note:** Only **root** can change file ownership.

***

#### Step 8 — Change Group with `chgrp`

```bash
sudo addgroup group2
sudo chown :group2 file1.txt
ls -l file1.txt
```

<p align="center"><img src="../../.gitbook/assets/image (203).png" alt=""></p>

***

### Assessment

Create `file1` and `file2` inside the Documents folder, then do the following:

**a.** Write text into `file1`:

```bash
cat >> file1    
I am Ahmed and I am a Cybersecurity student
```

**b.** List permissions of both files:

```bash
ls -l ~/Documents/file1 ~/Documents/file2
```

**c.** Grant write to group and read to all users on `file1`:

```bash
chmod g+w,a+r ~/Documents/file1
ls -l ~/Documents/file1
```

**d.** Copy `file1` permissions to `file2`:

```bash
chmod --reference=~/Documents/file1 ~/Documents/file2
```

**e.** List permissions of `file2`:

```bash
ls -l ~/Documents/file2
```
