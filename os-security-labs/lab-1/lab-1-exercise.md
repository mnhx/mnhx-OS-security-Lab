# Lab 1 Exercise

{% hint style="info" %}
**Note before start :** I recommend using **Metasploitable 2** instead of Ubuntu for this lab, as it is designed to be vulnerable and has many open ports ready for testing.
{% endhint %}

### 1- VM Configuration

If you using VirtualBox and going to use **your personal internet** make sure you use **'Nat Network'** to make isolate network for the server and clients

You can also use **'Host-only Adapter'** if you going to use **university internet**

<figure><img src="../../.gitbook/assets/image (50).png" alt=""><figcaption></figcaption></figure>

### Configuring the Virtual Machine Network:

<details>

<summary>How to create Nat Network in VirtualBox: </summary>

<div align="left"><figure><img src="../../.gitbook/assets/image (72).png" alt=""><figcaption></figcaption></figure> <figure><img src="../../.gitbook/assets/image (73).png" alt=""><figcaption></figcaption></figure> <figure><img src="../../.gitbook/assets/image (74).png" alt=""><figcaption></figcaption></figure></div>

You can change the Nat Network settings if you want

<figure><img src="../../.gitbook/assets/image (75).png" alt=""><figcaption></figcaption></figure>

</details>

<details>

<summary>How to create Nat Network in VMware:</summary>

After open the VMware press Edit then "Virtal Network Editor"

<figure><img src="../../.gitbook/assets/image (76).png" alt=""><figcaption></figcaption></figure>

<div><figure><img src="../../.gitbook/assets/image (77).png" alt=""><figcaption></figcaption></figure> <figure><img src="../../.gitbook/assets/image (78).png" alt=""><figcaption></figcaption></figure></div>

You can chose any Network number you want put only one can be the Nat

<figure><img src="../../.gitbook/assets/image (79).png" alt=""><figcaption></figcaption></figure>

Select Nat then edit the "Subnet IP" and "Subnet mask"

<figure><img src="../../.gitbook/assets/image (80).png" alt=""><figcaption></figcaption></figure>

then go to Nat Settings and edit the Gateway IP to Fit your Subnet IP

<figure><img src="../../.gitbook/assets/image (81).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (82).png" alt=""><figcaption></figcaption></figure>

Then press Apply ✅

{% hint style="info" %}
note: the same way if you going to create it for Host-only
{% endhint %}

After Finishing go to your VM and enter **"Edit virtual machine settings"**

<figure><img src="../../.gitbook/assets/image (83).png" alt=""><figcaption></figcaption></figure>

Then go to Network Adapter -> Select Custom and choose the same network number you configured

<figure><img src="../../.gitbook/assets/image (84).png" alt=""><figcaption></figcaption></figure>



</details>

### Lab Exercise :&#x20;

**Before starting, make sure both machines are connected to the same network and can communicate with each other. Use commands such as `ip a` or `ifconfig` to identify the IP address of each machine, then use the `ping` command to verify connectivity between them.**

<figure><img src="../../.gitbook/assets/image (27).png" alt=""><figcaption></figcaption></figure>

1- Send a flag between two machines using Netcat :&#x20;

open kali Linux and click on the kali icon and search for Wireshark

Choose **"eth0"** and press Enter

<div><figure><img src="../../.gitbook/assets/image (29).png" alt=""><figcaption></figcaption></figure> <figure><img src="../../.gitbook/assets/image (30).png" alt=""><figcaption></figcaption></figure></div>

Now go back and open terminal in the other machine and run:

`netcat -l -p 8000 -u -v`

> This command creates a listening connection on **port 8000** using **UDP**.

**Then open the terminal on the Kali Linux machine and run:**

`netcat <ip address> 8000 -u`

> Now, any message typed on the second machine will appear on the first machine.

Note: Flag meanings in the **Netcat command**

* **-u** → use **UDP** protocol
* **-p** → specify the **port number**
* **-l** → set **listen mode** (wait for incoming connection)
* **-v** → enable **verbose mode** (show connection details)

<figure><img src="../../.gitbook/assets/image (28).png" alt=""><figcaption></figcaption></figure>

as you can see here Whireshark catch the messages

<figure><img src="../../.gitbook/assets/image (32).png" alt="" width="563"><figcaption></figcaption></figure>

To save the **received** message into a file use:

`netcat <ip address> 8000 -u > output.txt`

**Note:** This file will only save the received messages, not the messages you send.

**Example in my case:**

* **Kali ⇒ Ubuntu ❌** (will not be saved)
* **Ubuntu ⇒ Kali ✅** (will be saved)

<figure><img src="../../.gitbook/assets/image (33).png" alt=""><figcaption></figcaption></figure>

### 2- Scan using Nmap capture it in Kali VM

First step,open kali Linux and click on the kali icon and search for Wireshark

Choose **"eth0"** and press Enter

<div><figure><img src="../../.gitbook/assets/image (29).png" alt=""><figcaption></figcaption></figure> <figure><img src="../../.gitbook/assets/image (30).png" alt=""><figcaption></figcaption></figure></div>

Second step, open the terminal in the host machine and run the **Nmap** command to scan the target machine:

```
nmap <target-ip>
```

<figure><img src="../../.gitbook/assets/image (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

{% hint style="info" %}
Note : No Open Ports Found

The scan showed 1000 closed ports because this is a fresh Ubuntu install. By default, Ubuntu does not run any services (like SSH or Web servers) for security reasons. Since no software is "listening" for connections, the system simply resets all Nmap attempts.

Recommendation: For penetration testing practice, I recommend using&#x20;

**Metasploitable 2** instead, as it is designed to be vulnerable and has many open ports ready for testing.
{% endhint %}
