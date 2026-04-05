---
description: >-
  Note : the downloading and setup will take long time make sure you do it
  before your class
---

# Windows Client

{% hint style="info" %}
**Note: It is recommended to use your Instructor ISO image. The one I shared may not work properly or could expire later.**
{% endhint %}

<details>

<summary>Windows 10 Pro: </summary>

[Link:](https://www.microsoft.com/en-us/software-download/windows10)

Product key :&#x20;

```
RHGJR-N7FVY-Q3B8F-KBQ6V-46YP4
```

After installing the **MediaCreationTool\_22H2** make sure you select the <mark style="color:$danger;">ISO file</mark>

<div><figure><img src="../../.gitbook/assets/image (64).png" alt=""><figcaption></figcaption></figure> <figure><img src="../../.gitbook/assets/image (65).png" alt=""><figcaption></figcaption></figure></div>

When you going creating New VM in VirtualBox make sure you turn off "**Proceed with Unattended Installation"**

<figure><img src="../../.gitbook/assets/image (66).png" alt=""><figcaption></figcaption></figure>

If the **product key** somehow didn't work you can select **"I don't have a product key"** both way will work with or without product key

<div><figure><img src="../../.gitbook/assets/image (67).png" alt=""><figcaption></figcaption></figure> <figure><img src="../../.gitbook/assets/image (68).png" alt=""><figcaption></figcaption></figure></div>

To make sure the you got the pro edition: search this PC and go to Properties

<div><figure><img src="../../.gitbook/assets/image (70).png" alt=""><figcaption></figcaption></figure> <figure><img src="../../.gitbook/assets/image (71).png" alt=""><figcaption></figcaption></figure></div>

</details>

<details>

<summary>Windows XP</summary>

[Link: ](https://archive.org/details/WinXPProSP3x86)

<figure><img src="../../.gitbook/assets/image (29) (1).png" alt=""><figcaption></figcaption></figure>

Product Key:&#x20;

{% hint style="info" %}
note: this Product key only work with **Windows XP Professional SP3 x86**
{% endhint %}

```
MRX3F-47B9T-2487J-KWKMF-RPWBY
```

Paste the Product key and make sure you don't forget the password&#x20;

[\[How store my password?\]](../lab-4/pre-installation-preparation.md#id-2.1-how-to-save-your-password)

<figure><img src="../../.gitbook/assets/image (30) (1).png" alt=""><figcaption></figcaption></figure>

</details>

<details>

<summary>Windows 7</summary>

[Link:](https://archive.org/details/windows-7-sp0-sp1-msdn-iso-files-en-de-ru-tr-x86-x64)

<figure><img src="../../.gitbook/assets/image (86).png" alt=""><figcaption></figcaption></figure>

If the activation message appears (usually after one month), click **Ask me later**.

<figure><img src="../../.gitbook/assets/image (3).png" alt=""><figcaption></figcaption></figure>

Then open **Command Prompt (CMD)** as **Administrator** and run:

```
slmgr -rearm
```

This resets the activation grace period and gives you another **30 days**.

> **Note:** You can usually repeat this more than once, for up to **120 days** in total, which should be enough to get through the semester.

</details>
