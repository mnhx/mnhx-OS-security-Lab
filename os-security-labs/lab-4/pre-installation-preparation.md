---
description: Installing windows server & Setting up the domain controller
---

# Pre-Installation Preparation

### 1- Windows Server 2012 and Product Keys:

<details>

<summary>installing Windows server</summary>

{% hint style="info" %}
**link:** [**windows server 2012**](https://www.microsoft.com/en-us/evalcenter/download-windows-server-2012-r2)
{% endhint %}

#### Product Keys :

```
H79BP-N24TR-MMRWX-9242F-8B3WM
D2N9P-3P6X9-2R39C-7RTCD-MDVJX
W3GGN-FT8W3-Y4M27-J84CP-Q3VJ9
```

</details>

### 2- VM Configuration

If you using VirtualBox and going to use your personal internet make sure you use **Nat Network** to make isolate network for the server and clients&#x20;

<figure><img src="../../.gitbook/assets/image (50).png" alt=""><figcaption></figcaption></figure>

after running the VM you should Chose Datacenter Evaluation (Server With GUI)

<div><figure><img src="../../.gitbook/assets/image (44).png" alt=""><figcaption><p><mark style="color:$danger;">1</mark></p></figcaption></figure> <figure><img src="../../.gitbook/assets/image (45).png" alt=""><figcaption><p><mark style="color:$danger;">2</mark></p></figcaption></figure></div>

Make sure you don't Forget the Password you use here or you will lose the VM

<figure><img src="../../.gitbook/assets/image (47).png" alt=""><figcaption></figcaption></figure>

#### 2.1- How to Save your Password:

I recommend using the **Description** feature in VirtualBox and VMware to safe the passwords

**VirtualBox :**&#x20;

Click on the VM -> Settings -> General -> Description

<div><figure><img src="../../.gitbook/assets/image (46).png" alt=""><figcaption></figcaption></figure> <figure><img src="../../.gitbook/assets/image (48).png" alt=""><figcaption></figcaption></figure></div>

#### VMware :&#x20;

<div align="left"><figure><img src="../../.gitbook/assets/Screenshot 2026-02-28 222616.png" alt="" width="257"><figcaption></figcaption></figure></div>

## Common errors:

<div><figure><img src="../../.gitbook/assets/image (38).png" alt=""><figcaption></figcaption></figure> <figure><img src="../../.gitbook/assets/image (39).png" alt=""><figcaption></figcaption></figure></div>

To solve it: turn off the VM and go to Settings -> System, and make sure the **Floppy** is selected

<div align="left"><figure><img src="../../.gitbook/assets/image (40).png" alt=""><figcaption></figcaption></figure></div>

Then go to Storage and selected the Floppy disk and click on **remove the attachment**

<div align="left" data-full-width="false"><figure><img src="../../.gitbook/assets/image (41).png" alt="" width="211"><figcaption></figcaption></figure></div>

then click on the iso image and select **Live CD/DVD**

<figure><img src="../../.gitbook/assets/image (43).png" alt=""><figcaption></figcaption></figure>

