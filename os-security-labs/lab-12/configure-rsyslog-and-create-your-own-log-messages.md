# Configure rsyslog and Create Your Own Log Messages

#### What is rsyslog?

The **rsyslog daemon** listens to log messages from different parts of the system and routes them to the correct log file in `/var/log`. It can also forward logs to a remote server.

Its main configuration file is at `/etc/rsyslog.conf`.

Each rule in the config file has two parts separated by a space:

```
facility.priority    /path/to/log/file
```

* **facility** → where the message comes from (the origin)
* **priority** → how serious the message is (the severity)

***

#### Facilities (Origin of the message)

| Facility             | Description                       |
| -------------------- | --------------------------------- |
| `auth` / `authpriv`  | Authorization and security events |
| `kern`               | Linux kernel messages             |
| `mail`               | Mail subsystem messages           |
| `cron`               | Cron daemon messages              |
| `daemon`             | Background service messages       |
| `news`               | Network news subsystem            |
| `lpr`                | Print-related messages            |
| `user`               | User program messages             |
| `local0` to `local7` | Reserved for local use            |

#### Priorities (Severity of the message)

| Priority | Description                                     |
| -------- | ----------------------------------------------- |
| `debug`  | Debug information from programs                 |
| `info`   | Simple informational message — no action needed |
| `notice` | Condition that may require attention            |
| `warn`   | Warning                                         |
| `err`    | Error                                           |
| `crit`   | Critical condition                              |
| `alert`  | Needs immediate intervention                    |
| `emerg`  | Emergency condition                             |

***

#### Selector Examples

| What you want                 | Rule to write                   |
| ----------------------------- | ------------------------------- |
| Log `warn` and above for mail | `mail.warn /var/log/mail.warn`  |
| Log all mail priorities       | `mail.* /var/log/mail.warn`     |
| Log only `info` priority      | `mail.=info /var/log/mail.warn` |
| Log all except `info`         | `mail.!info /var/log/mail.warn` |

***

#### Step 15 — Install rsyslog

```bash
apt install rsyslog
```

<figure><img src="../../.gitbook/assets/image (277).png" alt=""><figcaption></figcaption></figure>

Then start it:

```bash
systemctl start rsyslog
```

<p align="center"> <img src="../../.gitbook/assets/image (276).png" alt=""></p>

***

#### Step 16 — Enable rsyslog to Start Automatically

```bash
sudo systemctl enable --now rsyslog
```

This starts rsyslog immediately and makes it start automatically on every reboot.

***

#### Step 17 — Back Up the Config File Before Editing

Always make a backup before changing any configuration file.

```bash
cp /etc/rsyslog.conf /etc/rsyslog.conf.backup
```

***

#### Step 18 — Open the rsyslog Config File

```bash
vim /etc/rsyslog.conf
```

<p align="center"><img src="../../.gitbook/assets/image (278).png" alt=""></p>

You will see the full configuration including the `#### RULES ####` section. This is where log routing rules are defined.

> To exit VIM after editing, press `ESC` then type `:wq!` and press `Enter`. You can also press `ESC` then `SHIFT + ZZ`.

***

#### Step 19 — Add a Custom Log Rule

Inside the `#### RULES ####` section, add this line at the bottom:

```
local0.* /var/log/myapp.log
```

This tells rsyslog to write any message from the `local0` facility (at any priority) into `/var/log/myapp.log`.

Save and exit the file.

***

#### Step 20 — Restart rsyslog to Apply Changes

```bash
systemctl restart rsyslog
```

!\[Restarting rsyslog]\(images/restart\_rsyslog.png

Then check that it is running correctly:

```bash
systemctl status rsyslog
```

!\[rsyslog status showing active running]\(images/rsyslog\_status.png

You should see `Active: active (running)` in the output.

***

#### Step 21 — Test Your Log with the `logger` Utility

Use `logger` to send a test message to your new log file.

```bash
logger -p local0.info "critical error has Occurred 01/6/2030!"
```

!\[logger command with custom message]\(images/logger\_custom.png

> **Flag meanings:**
>
> * `-p` → specify the priority in `facility.priority` format

Now check that the message was recorded. You can verify it in the journal:

```bash
journalctl -f
```

!\[Custom log message visible in journalctl -f]\(images/logger\_journalctl\_verify.png

You will see your message appear in the live journal output.
