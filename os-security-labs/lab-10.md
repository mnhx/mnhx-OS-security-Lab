# Lab 10

### Objectives

* Understand policies related to accounts in Linux
* Apply account security policies in Linux platforms

{% hint style="warning" %}
**Before starting this lab, it is strongly recommended to take a snapshot of the virtual machine.**\
**This lab modifies account/PAM policy files, and a small mistake may lock the user account or prevent login.**\
**If anything goes wrong, the snapshot allows you to restore the system easily.**
{% endhint %}

***

### Before You Start

Linux stores account information across three key files:

* `/etc/passwd` → user account information
* `/etc/shadow` → password information (hashed)
* `/etc/group` → group information

***

### Lab Exercise

#### Step 1 — Check Your Current User Info

Before doing anything, run these commands to see who you are and what groups you belong to:

```bash
id
whoami
```

<p align="center"><img src="../.gitbook/assets/image (205).png" alt=""></p>

***

> **Note:** Always use `sudo` to run commands that require root privileges. Without it you will get a **Permission denied** error.

#### Step 2 — Update the System

First, update your system packages:

```bash
sudo apt update
```

<p align="center"><img src="../.gitbook/assets/image (206).png" alt=""></p>

***

#### Step 3 — Add a New User

Use `adduser` to create a new user. In this example we create a user called **salah**:

```bash
sudo adduser salah
```

```bash
sudo adduser samie
```

Follow the prompts to set a password and fill in the user information, then press **Y** to confirm.

<p align="center"><img src="../.gitbook/assets/image (207).png" alt=""></p>

> **Note:** When you create a new user, Linux automatically creates a group with the same name and adds the user to it.

Now switch to the new user to confirm it works:

```bash
su salah
```

Then switch back to your original user:

```bash
su kali
```

<p align="center"><img src="../.gitbook/assets/image (208).png" alt=""></p>

***

#### Step 4 — Add User to Sudoers

To give **salah** sudo privileges:

```bash
sudo usermod -aG sudo salah
```

Switch to salah and verify:

```bash
su salah
id
```

You should see `27(sudo)` in the groups list.

<p align="center"><img src="../.gitbook/assets/image (209).png" alt=""></p>

***

#### Step 5 — Delete a User

To delete a user, you need root. Without `sudo` it will be denied:

```bash
sudo userdel samie
```

Verify the user is removed by checking the passwd file:

```bash
cat /etc/passwd
```

<p align="center"><img src="../.gitbook/assets/image (210).png" alt=""></p>

<figure><img src="../.gitbook/assets/image (211).png" alt=""><figcaption></figcaption></figure>

***

#### Step 6 — View the /etc/passwd File

The `/etc/passwd` file holds basic info about every user on the system. Each line follows this format:

```
username:password:userid:groupid:user info:home path:shell
```

For example:

```
testuser:x:1481:1482:This is a test user:/home/testuser:/bin/bash
```

To view it:

```bash
cat /etc/passwd
```

<p align="center"><img src="../.gitbook/assets/image (213).png" alt=""></p>

***

#### Step 7 — View the /etc/shadow File

The `/etc/shadow` file stores the **hashed passwords** and password policy info. Each line follows this format:

```
username:password:lastchange:min:max:warn:inactive:expire:reserved
```

A regular user cannot read this file directly:

```bash
cat /etc/shadow
```

You will get **Permission denied**. Use `sudo`:

```bash
sudo cat /etc/shadow
```

<p align="center"><img src="../.gitbook/assets/image (214).png" alt=""></p>

> **Note:** The `max` field (default `99999`) controls how many days before the password expires. We will change this in the next step.

***

#### Step 8 — Change a User's Password

As a user, you can change your own password using:

```bash
passwd
```

You will be asked for your current password, then your new one.

<figure><img src="../.gitbook/assets/image (215).png" alt=""><figcaption></figcaption></figure>

> **Note:** Linux will reject the password if it is the same as the previous one, or if it is too short.
>
> You can change the password without knowing the current password if you have higher privilege

To check the current password policy for a user:

```bash
sudo chage -l salah
```

<p align="center"><img src="../.gitbook/assets/image (216).png" alt=""></p>

***

#### Step 9 — Enforce Password Change Every 60 Days

Use the `chage` command to set password expiry rules. No need to edit the shadow file manually.

Set the **maximum** number of days between password changes to **60**:

```bash
sudo chage -M 60 salah
```

Set the **minimum** number of days between password changes to **1**:

```bash
sudo chage -m 1 salah
```

Verify the change:

```bash
sudo chage -l salah
```

You should now see **Maximum: 60** and **Password expires** set to a future date.

<p align="center"><img src="../.gitbook/assets/image (217).png" alt=""></p>

***

#### Step 10 — Lock an Account After Too Many Failed Logins (PAM)

**PAM** stands for **Pluggable Authentication Modules**. It gives the system administrator control over authentication — logins, account access, passwords, and sessions.

PAM config files are in `/etc/pam.d`. The most important ones are:

* `common-auth` → handles authentication (counts failed attempts)
* `common-account` → handles account access (locks accounts)
* `common-password` → handles password rules
* `common-session` → handles sessions

Each line in a PAM file has this structure:

```
type   control-flag   PAM-module   <options>
```

**Types:**

* `auth` → manages authentication for user accounts
* `account` → manages user account validation
* `password` → manages passwords for user accounts
* `session` → manages sessions for user accounts

**Kinds of PAM modules used for locking:**

* `pam_tally` → older module, counts login attempts
* `pam_tally2` → updated version of pam\_tally
* `pam_faillock` → modern replacement, more flexible

List the PAM files to see what's available:

```bash
ls -l /etc/pam.d
```

<figure><img src="../.gitbook/assets/image (218).png" alt="" width="436"><figcaption></figcaption></figure>

***

**Step 10.1 — Edit common-auth**

Switch to root first:

```bash
su root
```

> **If you forget/don't know the root password use**
>
> `sudo passwd root`

Open the `common-auth` file:

```bash
vim /etc/pam.d/common-auth
```

<figure><img src="../.gitbook/assets/image (228).png" alt=""><figcaption></figcaption></figure>

Inside the file, add this line at the end of the auth block:

```
auth required pam_tally.so onerr=fail
```

<figure><img src="../.gitbook/assets/image (229).png" alt=""><figcaption></figcaption></figure>

Save and exit vim by pressing **Esc**, then typing `:wq` and pressing **Enter**.

To check if the configuration was saved, use:

```
grep -n "pam_tally" /etc/pam.d/common-auth
```

> **Note :** if you want to exit without saving :&#x20;
>
> Esc> \
> :q!> \
> Enter

***

**Step 10.2 — Edit common-account**

Now open the `common-account` file:

```bash
vim /etc/pam.d/common-account
```

<figure><img src="../.gitbook/assets/image (226).png" alt="" width="563"><figcaption></figcaption></figure>

Add this line at the beginning of the account block:

```
account required pam_tally.so deny=3 unlock_time=1800 reset
```

<figure><img src="../.gitbook/assets/image (243).png" alt=""><figcaption></figcaption></figure>

Save and exit.

***

To check if the configuration was saved, use:

```
grep -nE "pam_tally|deny=3|unlock_time=1800|reset" /etc/pam.d/common-auth /etc/pam.d/common-account
```

<figure><img src="../.gitbook/assets/image (244).png" alt=""><figcaption></figcaption></figure>

> **What this does:**
>
> * `deny=3` → lock the account after **3** failed login attempts
> * `unlock_time=1800` → keep the account locked for **30 minutes**&#x20;
>
> &#x20;      (1800 seconds)
>
> * `reset` → reset the counter after a successful login

> **Note:** If you do not reset the failed login counter, the system may still deny access even if the correct password is entered.\
> This is because PAM may still have recorded previous failed login attempts.
>
> To reset the failed login counter for the `kali` user, run:\
> `pam_tally --user kali --reset`                                   &#x20;
>
> Alternative commands if `pam_tally` is not found:
>
> `pam_tally2 --user --reset` &#x20;
>
> or
>
> `faillock --user --reset`

{% hint style="danger" %}
**Note:** Do not log out after this step, or you may not be able to log back in until the lockout time expires.\
If this happens, go to [**\[Step 11 — Reset Kali Password Without Login (GRUB Method)\]**](lab-10.md#step-11-reset-kali-password-without-login-grub-method)
{% endhint %}

***

**Step 10.3 — Create the Failure Log**

Now create the failure log file that `pam_tally` uses to track failed attempts:

```bash
touch /var/log/faillog
```

To view system-level errors in the log:

```bash
journalctl -b -p3
```

***

#### Step 11 — Reset Kali Password Without Login (GRUB Method)

Use this if you have forgotten your password and cannot log in.

**Step 11.1 — Reboot and Open GRUB**

Restart your machine. When the GRUB menu appears, press **E** to edit it.

<div><figure><img src="../.gitbook/assets/image (231).png" alt=""><figcaption></figcaption></figure> <figure><img src="../.gitbook/assets/image (232).png" alt=""><figcaption></figcaption></figure></div>

**Step 11.2 — Edit the Boot Line**

Scroll down until find the line that starts with `linux` and contains `ro quiet splash`. Make these two changes on that line:

1. Change `ro` → `rw`
2. Replace `quiet splash` → `init=/bin/bash`

Then press **Ctrl + X** to boot.

<div><figure><img src="../.gitbook/assets/image (233).png" alt=""><figcaption></figcaption></figure> <figure><img src="../.gitbook/assets/image (234).png" alt=""><figcaption></figcaption></figure></div>

**Step 11.3 — Reset Passwords**

Once you boot into the bash shell, reset the root password:

```bash
passwd
```

To reset another user's password:

```bash
passwd kali
passwd shawarma
passwd sngab 
```

<figure><img src="../.gitbook/assets/image (235).png" alt=""><figcaption></figcaption></figure>

**Step 11.4 — Reboot the Machine**

After changing the passwords, restart the system:

```bash
exec /sbin/init
```

Now log in with the new password.

**Common Error — Authentication token manipulation error:** If you see this error when running `passwd`, run this command first:

```bash
mount -o remount,rw /
```

Then try `passwd` again.

<figure><img src="../.gitbook/assets/image (242).png" alt=""><figcaption></figcaption></figure>

{% hint style="warning" %}
Recovery Note: If you are unable to log in after applying the PAM lockout settings, return to the GRUB bash shell and run the following commands to remove the `pam_tally` lines:
{% endhint %}

```bash
mount -o remount,rw /
sed -i '/pam_tally\.so/d' /etc/pam.d/common-auth
sed -i '/pam_tally\.so/d' /etc/pam.d/common-account
sync
exec /sbin/init
```

<figure><img src="../.gitbook/assets/image (241).png" alt=""><figcaption></figcaption></figure>

***

### **Addition ,Ubuntu users:**

When booting, hold **`Shift`** to enter the GRUB menu.&#x20;

<figure><img src="../.gitbook/assets/image (236).png" alt=""><figcaption></figcaption></figure>

Then click **`E`** while highlighting the Ubuntu option, and hold the down arrow to scroll to "linux"

<figure><img src="../.gitbook/assets/image (238).png" alt=""><figcaption></figcaption></figure>

Find the line that starts with `linux` and contains `ro quiet splash`.

Make these two changes on that line:

1. Change `ro` → `rw`
2. Replace `quiet splash` → `init=/bin/bash`

Then press **Ctrl + X** to boot.

<div><figure><img src="../.gitbook/assets/image (239).png" alt=""><figcaption></figcaption></figure> <figure><img src="../.gitbook/assets/image (240).png" alt=""><figcaption></figcaption></figure></div>
