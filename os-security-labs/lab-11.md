# Lab 11

### Access Control List (ACL) in Linux

In Linux, file security is managed through two main systems: the traditional **standard permission policy** and the more flexible **Access Control Lists (ACLs)**.

* Use **Standard Permissions** for basic tasks where you only need one owner and one primary group.
* Use **ACLs** when a specific user or service account needs access to a file it does not own.

ACLs allow you to assign permissions to individual users or groups, even if they are not the original owner or owning group. This lets you build complex access scenarios without changing the application logic.

***

### Lab Exercise

#### Step 1 — Install the ACL Tools

Make sure ACL tools are installed on your Linux system.

```bash
sudo apt-get install acl
```

This installs the `getfacl` and `setfacl` commands.

***

#### Step 2 — Activate ACL on the Main Partition

```bash
sudo mount -o remount,acl /
```

This re-mounts your root partition with ACL support enabled.

***

#### Step 3 — Create a New Directory

Switch to root first, then create a new directory called `lab11`.

```bash
sudo su
mkdir lab11
ls -l
```

<figure><img src="../.gitbook/assets/image (250).png" alt="" width="398"><figcaption></figcaption></figure>

> The directory `lab11` is now owned by **root**. You can confirm this with `ls -l`.

***

#### Step 4 — Create a New User "Adam"

Switch back to a normal user, then add the new user.

```bash
sudo adduser adam
```

<figure><img src="../.gitbook/assets/image (252).png" alt="" width="400"><figcaption></figcaption></figure>

Follow the prompts to set a password and fill in the details (you can press Enter to skip optional fields).

After creating the user, confirm it was added by listing home directories:

```bash
ls /home
```

You should see `adam` listed alongside other users.

***

#### Step 5 — Create a Group and Add Adam to It

Create a group called `cys504` and add `adam` to it.

```bash
sudo addgroup cys311
sudo usermod -aG cys311 adam
```

Verify that `adam` is now part of `cys504`:

```bash
groups adam
```

You should see: `adam : adam cys311`

You can also double-check by searching the group file:

```bash
cat /etc/group | grep cys311
```

Expected output: `cys311:x:1006:adam`

<figure><img src="../.gitbook/assets/image (254).png" alt="" width="456"><figcaption></figcaption></figure>

> Here `cys311` is the group name, `x` is the group password placeholder, `1006` is the Group ID (GID), and `adam` is the member.

***

#### Step 6 — Change Group Ownership of the Directory

Make `cys311` the owning group of the `lab11` directory.

```bash
chown -R :cys311 lab11
ls -l
```

<figure><img src="../.gitbook/assets/Screenshot 2026-06-05 234017 (1).png" alt="" width="483"><figcaption></figcaption></figure>

You should now see `cys311` as the group owner of `lab11`.

***

#### Step 7 — Try to Create a File as Adam (Permission Denied)

Switch to user `adam` and navigate into `lab11`, then try to create a file.

```bash
su adam
cd /home/kali/lab11
touch file1
```

<figure><img src="../.gitbook/assets/Screenshot 2026-06-05 235050.png" alt="" width="509"><figcaption></figcaption></figure>

You will see:

```
touch: cannot touch 'file1': Permission denied
```

This happens because `adam` does not have **write (w)** permission for this directory yet.

***

#### Step 8 — View the Current ACL

Go back to root and check the current ACL state of the directory.

```bash
su root
getfacl lab11
```

<figure><img src="../.gitbook/assets/image (256).png" alt="" width="525"><figcaption></figcaption></figure>

&#x20;The output will show the default Unix permissions with no extended ACL entries for `adam` yet.

> `getfacl` → check the current state of the ACL for a file or directory.

***

#### Step 9 — Grant Adam Access Using ACL

From the root shell, use `setfacl` to give `adam` full permissions on `lab11`.

```bash
setfacl -m u:adam:rwx /home/kali/lab11
```

> **Flag meanings:**
>
> * `-m` → modify the ACL
> * `u:adam:rwx` → give user `adam` read, write, and execute permissions
> * If it didn't work try :&#x20;

```bash
setfacl -R -m u:adam:rwx /home/kali/lab11
```

***

#### Step 10 — Verify Adam Can Now Create Files

Switch to `adam` again and try creating the file.

```bash
su adam
cd /home/kali/lab11
touch file1
ls -l
```

<figure><img src="../.gitbook/assets/image (257).png" alt="" width="465"><figcaption></figcaption></figure>

This time it works. You can see `file1` listed with `adam` as the owner.

***

#### Step 11 — View the Updated ACL

Switch back to root and view the ACL again to see what changed.

```bash
su root
getfacl lab11
```

<figure><img src="../.gitbook/assets/image (258).png" alt="" width="425"><figcaption></figcaption></figure>

```
user:adam:rwx
```

This shows that `adam` has been given explicit `rwx` permissions through the ACL — while other users remain restricted.

> The `mask::rwx` line also appears. The mask limits the maximum permissions that named users, named groups, and the owning group can have.

***

#### Step 12 — Confirm Other Users Are Still Blocked

Switch to another user (for example, `ahmed`) and try to create a file inside `lab11`.

```bash
su ahmed
cd /home/kali/lab11
touch file2
```

<figure><img src="../.gitbook/assets/image (259).png" alt="" width="518"><figcaption></figcaption></figure>

You will see:

```
touch: cannot touch 'file2': Permission denied
```

This confirms that only `adam` has access through the ACL, and all other users are still restricted.

***

#### Step 13 — Remove a User's ACL Permission

To remove `adam`'s ACL entry specifically, use `setfacl -x`.

```bash
setfacl -x "adam" lab11
getfacl lab11
```

<figure><img src="../.gitbook/assets/image (260).png" alt="" width="378"><figcaption></figcaption></figure>

The `user:adam:rwx` line is now gone. Adam no longer has the extra permission.

Confirm that `adam` is blocked again:

```bash
su adam
cd /home/kali/lab11
touch file3
```

<figure><img src="../.gitbook/assets/image (261).png" alt="" width="323"><figcaption></figcaption></figure>

<pre><code><strong>touch: cannot touch 'file3': Permission denied
</strong></code></pre>

***

#### Step 14 — Remove the Complete ACL

To remove **all** ACL entries from `lab11` entirely, use `setfacl -b`.

```bash
setfacl -b lab11
getfacl lab11
```

<figure><img src="../.gitbook/assets/image (262).png" alt="" width="431"><figcaption></figcaption></figure>

**Before removing all ACL:**

```
user::rwx
user:ahmed:rwx
group::rwx
mask::rwx
other::r-x
```

**After removing all ACL (`setfacl -b`):**

```
user::rwx
group::r-x
other::r-x
```

> `setfacl -b` → remove the **complete** ACL, leaving only the standard Unix permissions.

***

### ACL Entry Types — Quick Reference

| Type         | Text Form        |
| ------------ | ---------------- |
| owner        | `user::rwx`      |
| named user   | `user:name:rwx`  |
| owning group | `group::rwx`     |
| named group  | `group:name:rwx` |
| mask         | `mask::rwx`      |
| other        | `other::rwx`     |

***

### Commands Summary

| Command                                | What it does                     |
| -------------------------------------- | -------------------------------- |
| `sudo apt-get install acl`             | Install ACL tools                |
| `sudo mount -o remount,acl /`          | Activate ACL on main partition   |
| `getfacl <directory>`                  | View current ACL                 |
| `setfacl -m u:name:rwx <directory>`    | Add/modify user ACL entry        |
| `setfacl -x "name" <directory>`        | Remove a specific user ACL entry |
| `setfacl -b <directory>`               | Remove the entire ACL            |
| `setfacl -R -m u:name:rwX <directory>` | Apply ACL recursively            |

***
