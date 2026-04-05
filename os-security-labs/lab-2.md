# Lab 2

### 1- VM Configuration

If you using VirtualBox and going to use your personal internet make sure you use **Nat Network** to make isolate network for the server and clients

<figure><img src="../.gitbook/assets/image (50).png" alt=""><figcaption></figcaption></figure>

### Configuring the Virtual Machine Network:

<details>

<summary>How to create Nat Network in VirtualBox: </summary>

<div align="left"><figure><img src="../.gitbook/assets/image (72).png" alt=""><figcaption></figcaption></figure> <figure><img src="../.gitbook/assets/image (73).png" alt=""><figcaption></figcaption></figure> <figure><img src="../.gitbook/assets/image (74).png" alt=""><figcaption></figcaption></figure></div>

You can change the Nat Network settings if you want

<figure><img src="../.gitbook/assets/image (75).png" alt=""><figcaption></figcaption></figure>

</details>

<details>

<summary>How to create Nat Network in VMware:</summary>

After open the VMware press Edit then "Virtal Network Editor"

<figure><img src="../.gitbook/assets/image (76).png" alt=""><figcaption></figcaption></figure>

<div><figure><img src="../.gitbook/assets/image (77).png" alt=""><figcaption></figcaption></figure> <figure><img src="../.gitbook/assets/image (78).png" alt=""><figcaption></figcaption></figure></div>

You can chose any Network number you want put only one can be the Nat

<figure><img src="../.gitbook/assets/image (79).png" alt=""><figcaption></figcaption></figure>

Select Nat then edit the "Subnet IP" and "Subnet mask"

<figure><img src="../.gitbook/assets/image (80).png" alt=""><figcaption></figcaption></figure>

then go to Nat Settings and edit the Gateway IP to Fit your Subnet IP

<figure><img src="../.gitbook/assets/image (81).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/image (82).png" alt=""><figcaption></figcaption></figure>

Then press Apply ✅

{% hint style="info" %}
note: the same way if you going to create it for Host-only
{% endhint %}

After Finishing go to your VM and enter **"Edit virtual machine settings"**

<figure><img src="../.gitbook/assets/image (83).png" alt=""><figcaption></figcaption></figure>

Then go to Network Adapter -> Select Custom and choose the same network number you configured

<figure><img src="../.gitbook/assets/image (84).png" alt=""><figcaption></figcaption></figure>



</details>

### Lab Exercise :&#x20;

#### **1- armitage**&#x20;

First, switch to the root user using `sudo su` (to gain full privileges).\
&#x20;Then start PostgreSQL using `/etc/init.d/postgresql start` (required for the database). \
After that, run `msfdb init` (to initialize the database if needed), \
and finally execute `armitage` (to launch the graphical interface).

<figure><img src="../.gitbook/assets/image (172).png" alt=""><figcaption></figcaption></figure>

Don't change anything here : <br>

<figure><img src="../.gitbook/assets/image (173).png" alt=""><figcaption></figcaption></figure>

First we will add Host (I will using [Metasploitable 2](https://sourceforge.net/projects/metasploitable/))

<div><figure><img src="../.gitbook/assets/image (176).png" alt=""><figcaption></figcaption></figure> <figure><img src="../.gitbook/assets/image (184).png" alt=""><figcaption></figcaption></figure> <figure><img src="../.gitbook/assets/image (183).png" alt=""><figcaption></figcaption></figure></div>

{% hint style="info" %}
if the host didn't show up try add it again
{% endhint %}

After adding the target host, select it and run **Nmap Scan → Quick Scan (OS Detect)** to identify the operating system and gather basic information about the target.

<div><figure><img src="../.gitbook/assets/image (185).png" alt=""><figcaption></figcaption></figure> <figure><img src="../.gitbook/assets/image (186).png" alt=""><figcaption></figcaption></figure></div>

Now we going to search for exploit using find attack

<div><figure><img src="../.gitbook/assets/image (187).png" alt=""><figcaption></figcaption></figure> <figure><img src="../.gitbook/assets/image (188).png" alt=""><figcaption></figcaption></figure></div>

We will use the exploit which is exploit/unix/ftp/vsftpd\_2.3.4 \
Make sure you set the `RHOST` (target host) to the target machine’s IP address, and the `LHOST` (local host) to your own device’s IP address correctly after that press Launch.

<div><figure><img src="../.gitbook/assets/image (189).png" alt=""><figcaption></figcaption></figure> <figure><img src="../.gitbook/assets/image (190).png" alt=""><figcaption></figcaption></figure></div>

After the exploit is completed, we can see that a shell session has been successfully opened on the target system.

<figure><img src="../.gitbook/assets/image (191).png" alt=""><figcaption></figcaption></figure>

Now, for post-exploitation, we will interact with the compromised system to gain control over the target device.

<figure><img src="../.gitbook/assets/image (192).png" alt=""><figcaption></figcaption></figure>

As we can see here, we can interact with the shell to control the target device. The output below shows the directories and files in the Metasploitable:

<figure><img src="../.gitbook/assets/image (193).png" alt=""><figcaption></figcaption></figure>

#### **2 - Penetration Testing with Metasploit Rationale**

&#x20;Start by making sure that both devices are on the same network.&#x20;

<div><figure><img src="../.gitbook/assets/image (194).png" alt=""><figcaption></figcaption></figure> <figure><img src="../.gitbook/assets/image (183).png" alt=""><figcaption></figcaption></figure></div>

Then, perform an Nmap scan on the target device to identify open ports and potential vulnerabilities.

<figure><img src="../.gitbook/assets/image (195).png" alt=""><figcaption></figcaption></figure>

> Note : -sV : Detect service versions running on open ports
>
> -T5 : Use very fast/aggressive timing (faster scan but less stealthy)

Now we will check whether **vsftpd 2.3.4** has a known vulnerability or exploit in Metasploit or Exploit-DB using the `searchsploit` command.

<figure><img src="../.gitbook/assets/image (196).png" alt=""><figcaption></figcaption></figure>

As we can see, the service is vulnerable and there is a corresponding exploit available in Metasploit. Therefore, we will use this exploit to gain access to the target machine\
first we search for the  **vsftpd 2.3.4** exploit \
then setting the `RHOST` and then executing the `run` command.\
\
After gaining access, we will verify our access by checking the current user to confirm that we are inside the target system.

<figure><img src="../.gitbook/assets/image (201).png" alt=""><figcaption></figcaption></figure>

If a session is opened but you are not automatically interacting with it, you can use the **`sessions`** command to check if it is still active. Then, use **`sessions -i <session_number>`** to manually interact with the session.

> **Note:** You can use the **`background`** command to move the current session to the background without closing it, so you can interact with it later.

<figure><img src="../.gitbook/assets/image (202).png" alt=""><figcaption></figcaption></figure>

### **Common Error :**&#x20;

This issue is very common when using the **vsftpd\_2.3.4\_backdoor exploit**. The message indicates that the exploit has “completed” (Exploit completed), but no session was created.

<figure><img src="../.gitbook/assets/image (197).png" alt=""><figcaption></figcaption></figure>

Open another terminal and run **`sudo netstat -antp | grep 6200`** to identify the process using port 6200. After finding the process ID (PID), terminate it using **`sudo kill -9 <PID>`**.

<figure><img src="../.gitbook/assets/image (200).png" alt=""><figcaption></figcaption></figure>

Now go back to msfconsole and try again:

