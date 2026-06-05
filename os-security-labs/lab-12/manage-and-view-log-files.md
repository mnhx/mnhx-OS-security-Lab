# Manage and View Log Files

Linux and the applications that run on it can generate all different types of messages, which are recorded in various log files. Linux uses a set of configuration files, directories, programs, commands and daemons to create, store and recycle these log messages. Knowing where the system keeps its log files and how to make use of related commands can therefore help save valuable time during digital investigation.

***

#### Step 1 — Switch to Root and Go to the Log Directory

Switch to the root user first, then navigate into the log directory.

```bash
sudo su
cd /var/log
ls -l
```

<figure><img src="../../.gitbook/assets/image (263).png" alt="" width="468"><figcaption></figcaption></figure>

This lists all the log files stored on the system. You will see files like `wtmp`, `btmp`, `auth.log`, `boot.log`, `kern.log`, and many others.

***

#### Step 2 — Common Log Files

Here are some important log files you will find under `/var/log`:

| File                   | What it stores                            |
| ---------------------- | ----------------------------------------- |
| `wtmp`                 | Binary log of all login and logout events |
| `btmp`                 | Failed login attempts                     |
| `utmp`                 | Current login sessions                    |
| `dmesg`                | Kernel boot messages                      |
| `messages`             | General system messages                   |
| `maillog` / `mail.log` | Mail-related messages                     |
| `spooler`              | Print spool messages                      |
| `auth.log` / `secure`  | Authentication and security events        |
| `boot.log`             | Messages generated during system boot     |
| `kern.log`             | Kernel messages                           |
| `user.log`             | Messages from user-level programs         |

> `wtmp` and `utmp` are **binary files** — you cannot read them directly with `cat`. You need to use specific commands for that.

***

#### Step 3 — Try Reading wtmp with cat (What Happens)

```bash
cat wtmp
```

<p align="center"><img src="../../.gitbook/assets/image (264).png" alt="" data-size="original"></p>

You will see random unreadable characters. This is because `wtmp` is a binary file and `cat` cannot display it properly.

***

#### Step 4 — Read wtmp Properly Using the `last` Command

The `last` command reads `wtmp` and shows the login history in a readable format.

```bash
last
```

<p align="center"><img src="../../.gitbook/assets/image (265).png" alt=""></p>

> `last` → reads from `/var/log/wtmp` and shows who logged in, when, and for how long.

You can also limit how many results you see using numbers:

```bash
last -1
```

This shows only the most recent login.

```bash
last -2
```

This shows the last 2 logins.

```bash
last -5
```

This shows the last 5 logins.

```bash
last -a
```

This shows all logins with the hostname displayed in the last column.

<p align="center"><img src="../../.gitbook/assets/image (266).png" alt=""></p>

To see all available options for `last`:

```bash
last --help
```

<p align="center"><img src="../../.gitbook/assets/image (267).png" alt=""></p>

> **Useful `last` flags:**
>
> * `-a` → display hostnames as last entry
> * `-F` → display full login and logout times and dates
> * `-n N` → show only N lines
> * `-s` → display lines since the specified time
> * `-t` → display lines until the specified time
> * `-x` → display system shutdown entries and run level changes

***

#### Step 6 — See Who Is Currently Logged In

```bash
who
```

This shows all users currently logged in to the system. It reads its values from `/run/utmp`.

***

#### Step 5 — Check Reboot History

```bash
last reboot
```

<figure><img src="../../.gitbook/assets/image (268).png" alt="" width="468"><figcaption></figcaption></figure>

This shows every time the system was rebooted.

***

#### Step 7 — View Last Login of Each User Using `lastlog2`

First, install `lastlog2` if it is not already installed:

```bash
apt update
apt install lastlog2
```

<p align="center"><img src="../../.gitbook/assets/image (269).png" alt=""></p>

Then run it:

```bash
lastlog2
```

<p align="center"><img src="../../.gitbook/assets/image (270).png" alt=""></p>

This shows each user account, the terminal they used, and the exact date and time of their most recent login.

***

#### Step 8 — View the Boot Log

Read the last few lines of `boot.log` to see the most recent boot events:

```bash
tail boot.log
```

<p align="center"><img src="../../.gitbook/assets/image (273).png" alt=""></p>

To see the entire boot log:

```bash
cat boot.log
```

<figure><img src="../../.gitbook/assets/image (279).png" alt="" width="416"><figcaption></figcaption></figure>

***

#### Step 9 — Save Kernel Messages to a File Using dmesg

```bash
dmesg > ~/boot.dmesg1
```

This saves all kernel messages into a file called `boot.dmesg1` in your home directory.

```bash
cat ~/boot.dmesg1
```

<p align="center"><img src="../../.gitbook/assets/image (272).png" alt=""></p>

***

#### Step 10 — View Logs Using journalctl

The `journalctl` command reads logs from the **systemd journal** — the modern log system on most Linux distributions.

```bash
journalctl
```

<figure><img src="../../.gitbook/assets/image (274).png" alt="" width="468"><figcaption></figcaption></figure>

To follow new log entries in real time:

```bash
journalctl -f
```

<p align="center"><img src="../../.gitbook/assets/image (275).png" alt=""></p>

Press `Ctrl + C` to stop following.

You can also filter by a specific service. For example, to watch SSH and login events at the same time:

```bash
journalctl -f -t sshd -t systemd-logind
```

***

#### Step 11 — Read the auth.log File

The `auth.log` file records all authentication events — login attempts, password failures, and sudo usage.

```bash
tail -f auth.log
```

!\[tail -f auth.log showing live authentication events]\(images/tail\_auth\_log.png

This will keep streaming new entries as they happen. Press `Ctrl + C` to stop.

> You can clearly see failed login attempts and `su` authentication failures in this log. This is very useful for detecting unauthorized access attempts.

***

#### Step 12 — Read the user.log File

```bash
cat /var/log/user.log
```

!\[cat /var/log/user.log output]\(images/cat\_user\_log.png

This shows messages from user-level programs running on the system.

***

#### Step 13 — Follow the syslog in Real Time

```bash
tail -f /var/log/syslog
```

!\[tail -f /var/log/syslog output]\(images/tail\_syslog.png

This streams all general system messages as they are written. Press `Ctrl + C` to stop.

***

#### Step 14 — Test Sending a Log Message with `logger`

The `logger` command lets you manually send a message to the system log. This is useful for testing.

```bash
logger hello world
```

Then check that it appeared in the journal:

```bash
journalctl -f
```

!\[logger hello world visible in journalctl]\(images/logger\_basic.png

You will see your message appear as a new log entry.
