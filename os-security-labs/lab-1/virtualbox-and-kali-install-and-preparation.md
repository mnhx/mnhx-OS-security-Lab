---
description: Installing VirtualBox & Kali Linux and Ubuntu
---

# VirtualBox & Kali Install and Preparation

### 1- VirtualBox installation:

[Link:](https://www.virtualbox.org/wiki/Downloads)

**Choose the platform packages for your OS.**

<figure><img src="../../.gitbook/assets/image (34).png" alt="" width="563"><figcaption></figcaption></figure>

Make sure you selected **"VirtualBox Application".**

<figure><img src="../../.gitbook/assets/image (1) (1) (1) (1) (1).png" alt="" width="563"><figcaption></figcaption></figure>

### 2- Kali Linux Install :&#x20;

[link:](https://www.kali.org/get-kali/#kali-virtual-machines)

Choose the version that matches your virtualization software (e.g., **VirtualBox** or **VMware**).

Click the download icon to start downloading the file.

<figure><img src="../../.gitbook/assets/image (2) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

**After extracting the compressed file, you will find two files inside the folder: a .vbox file and a .vdi file.**

<figure><img src="../../.gitbook/assets/image (4) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

Open VirtualBox and import the Kali Linux virtual machine

Click on Machines ⇒ New<br>

<figure><img src="../../.gitbook/assets/image (5) (1) (1).png" alt="" width="563"><figcaption></figcaption></figure>

**Write the name of the machine and select:**

* **OS:** Linux
* **OS Distribution:** Debian
* **OS Version:** Debian (64-bit)

<figure><img src="../../.gitbook/assets/image (6) (1) (1).png" alt=""><figcaption></figcaption></figure>

**For specifying virtual hardware:**

* **Base Memory (RAM):** 2 GB is Minimal.
* **Number of CPUs:** 3–4 CPUs are enough.

{% hint style="info" %}
**Note:** These are the standard requirements for smooth operation of the OS. If you want to allocate more resources, do **not exceed the green bar** in the VirtualBox/VMware settings.
{% endhint %}

<figure><img src="../../.gitbook/assets/image (7) (1) (1).png" alt=""><figcaption></figcaption></figure>

**If you want to change the location where the virtual machine will store its disk, click on the folder/file icon.**

**The minimal disk size should be between 8 GB and 20 GB.**

{% hint style="info" %}
**Note:** If you have extended storage, it is recommended to use it for the virtual machine's hard disk.
{% endhint %}

<figure><img src="../../.gitbook/assets/image (8) (1) (1).png" alt=""><figcaption></figcaption></figure>

After you finish , right click on your machine and press settings.

<figure><img src="../../.gitbook/assets/image (9) (1) (1).png" alt=""><figcaption></figcaption></figure>

Go to **Display** and change Video Memory from 16 to 128 MB.

<figure><img src="../../.gitbook/assets/image (10) (1) (1).png" alt="" width="563"><figcaption></figcaption></figure>

Now go to Storage ⇒ Controller: IDE then press this icon.

<figure><img src="../../.gitbook/assets/image (11) (1) (1).png" alt=""><figcaption></figcaption></figure>

Select **"Add"**, then navigate to the folder where you extracted the compressed file and select the Kali Linux .vdi file.&#x20;

<figure><img src="../../.gitbook/assets/image (12) (1).png" alt=""><figcaption></figcaption></figure>

{% hint style="info" %}
Note: The same steps can be used to set up any virtual machine that uses a VDI file
{% endhint %}

After starting the virtual machine, log in using the username `kali` and the password `kali`.

<figure><img src="../../.gitbook/assets/image (13) (1).png" alt=""><figcaption></figcaption></figure>

### 3- Download other Linux distribution

<details>

<summary>Ubuntu</summary>

[Link:](https://ubuntu.com/download/desktop)

{% hint style="info" %}
**Note: Ubuntu LTS and the standard Ubuntu versions usually have large file sizes, typically ranging from 5.3 GB to 6.5 GB.**
{% endhint %}

<figure><img src="../../.gitbook/assets/image (2) (1) (1).png" alt=""><figcaption></figcaption></figure>

After download, open VirtualBox and import the Ubuntu virtual machine.

Click on Machines ⇒ New

<figure><img src="../../.gitbook/assets/image (5) (1) (1).png" alt=""><figcaption></figcaption></figure>

Open the **"ISO Image"** option, select "Other", then choose the ISO image you downloaded.

<figure><img src="../../.gitbook/assets/image (3) (1) (1).png" alt=""><figcaption></figcaption></figure>

make sure you uncheck the "Proceed with Unattended Installation" option.

<figure><img src="../../.gitbook/assets/image (4) (1) (1).png" alt=""><figcaption></figcaption></figure>

**Write the name of the machine and select:**

* **OS:** Linux
* **OS Distribution:** Ubuntu
* **OS Version:** Ubuntu (64-bit)

<figure><img src="../../.gitbook/assets/image (5) (1).png" alt=""><figcaption></figcaption></figure>

**For specifying virtual hardware:**

* **Base Memory (RAM): 4 GB is recommended.**
* **Number of CPUs: 3–4 CPUs are sufficient**

<figure><img src="../../.gitbook/assets/image (7) (1).png" alt=""><figcaption></figcaption></figure>

**The minimal disk size should be 20 GB.**

{% hint style="info" %}
Note: The same steps can be used to set up any virtual machine that uses an **ISO** file
{% endhint %}

**\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_**

After you finish , right click on your machine and press settings.\
Go to **Display** and change Video Memory from 16 to 128 MB.

<figure><img src="../../.gitbook/assets/image (8) (1).png" alt=""><figcaption></figcaption></figure>

After starting the virtual machine, choose **"Try or Install Ubuntu"**

<figure><img src="../../.gitbook/assets/image (10) (1).png" alt=""><figcaption></figcaption></figure>

Choose **"Use wired connection"**

<figure><img src="../../.gitbook/assets/image (11) (1).png" alt=""><figcaption></figcaption></figure>

You can skip the Update if you want

<figure><img src="../../.gitbook/assets/image (12).png" alt=""><figcaption></figcaption></figure>

Choose **"Install Ubuntu"** then select **"Interactive installation"**

<div><figure><img src="../../.gitbook/assets/image (18).png" alt=""><figcaption></figcaption></figure> <figure><img src="../../.gitbook/assets/image (19).png" alt=""><figcaption></figcaption></figure></div>

You can choose **"Extended Selection"** if needed, but we will proceed with the default option.

<figure><img src="../../.gitbook/assets/image (15).png" alt=""><figcaption></figcaption></figure>

Make sure you check Install third-party software for graphics and Wi-fi hardware to avoid errors

<figure><img src="../../.gitbook/assets/image (16).png" alt=""><figcaption></figcaption></figure>

Choose **"Erase disk and install Ubuntu"** (won't erase your disk, don't worry)

<figure><img src="../../.gitbook/assets/image (17).png" alt=""><figcaption></figcaption></figure>

After setting your username and selecting the time zone, click "Install" to start the installation process when you should restart the machine.

### Additional note:

&#x20;If the system installation process freezes, try repeating the installation without an internet connection. This usually resolves the issue.

<figure><img src="../../.gitbook/assets/image (20).png" alt=""><figcaption></figcaption></figure>

</details>

<details>

<summary>Metasploitable 2</summary>

[Link:](https://sourceforge.net/projects/metasploitable/)

Click the download icon to start downloading the file.

<figure><img src="../../.gitbook/assets/image (21).png" alt=""><figcaption></figcaption></figure>

After extracting the compressed file, you will find two files inside the folder:  a **.vmdk** file

<figure><img src="../../.gitbook/assets/image (22).png" alt=""><figcaption></figcaption></figure>

Open VirtualBox and import the Metasploitable 2 virtual machine

Click on Machines ⇒ New

<figure><img src="../../.gitbook/assets/image (5) (1) (1).png" alt=""><figcaption></figcaption></figure>

**Write the name of the machine and select:**

* **OS:** Linux
* **OS Distribution:** **Ubuntu**
* **OS Version:** **Ubuntu** (64-bit)

<figure><img src="../../.gitbook/assets/image (23).png" alt=""><figcaption></figcaption></figure>

**For specifying virtual hardware:**

* **Base Memory (RAM):** 1 GB is enough.
* **Number of CPUs:** 1 CPUs are enough.

<figure><img src="../../.gitbook/assets/image (24).png" alt=""><figcaption></figcaption></figure>

**2 GB should be enough as disk size.**

<figure><img src="../../.gitbook/assets/image (25).png" alt=""><figcaption></figcaption></figure>

After you finish , right click on your machine and press settings.

Now go to Storage ⇒ Controller: IDE then press this icon.

<figure><img src="../../.gitbook/assets/image (11) (1) (1).png" alt=""><figcaption></figcaption></figure>

Select **"Add"**, then navigate to the folder where you extracted the compressed file and select the **.vmdk** file.&#x20;

<figure><img src="../../.gitbook/assets/image (22).png" alt=""><figcaption></figcaption></figure>

After starting the virtual machine, log in using the username `msfadmin` and the password `msfadmin`.

<figure><img src="../../.gitbook/assets/image (26).png" alt=""><figcaption></figcaption></figure>

</details>

#### How to Save your Password:

I recommend using the **Description** feature in VirtualBox and VMware to safe the passwords

**VirtualBox :**&#x20;

Click on the VM -> Settings -> General -> Description

<div><figure><img src="../../.gitbook/assets/image (46).png" alt=""><figcaption></figcaption></figure> <figure><img src="../../.gitbook/assets/image (48).png" alt=""><figcaption></figcaption></figure></div>

#### VMware :&#x20;

<div align="left"><figure><img src="../../.gitbook/assets/Screenshot 2026-02-28 222616.png" alt="" width="257"><figcaption></figcaption></figure></div>

