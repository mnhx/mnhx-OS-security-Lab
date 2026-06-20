# File and Folder Sharing

This section introduces file and folder sharing within a domain environment.

A shared folder is created and access is controlled using both Share permissions and NTFS permissions. The effective access granted to a user depends on the most restrictive combination of these permissions.<br>

### 1- Shared Folder Configuration on the Server

1- Creating the shared folder in the server root (usually the best location)

<figure><img src="../../.gitbook/assets/image (147).png" alt=""><figcaption></figcaption></figure>

2- Go to Sharing then click on "Share"\
![](<../../.gitbook/assets/image (160).png>)

Write the Group name then press "Add" and make the Permission Level as "Read" for the group then press "Share"

<div><figure><img src="../../.gitbook/assets/image (99).png" alt="" width="563"><figcaption></figcaption></figure> <figure><img src="../../.gitbook/assets/image (100).png" alt="" width="473"><figcaption></figcaption></figure></div>

Note: It is possible to assign permissions directly to a user instead of a group. However, using groups is considered best practice. In this lab, the user was added directly to ensure they have "Read/Write" permissions that are higher than other users.

### Additional :

Check "Advance Sharing" Make sure that the “Share this folder” option is enabled.

<figure><img src="../../.gitbook/assets/image (169).png" alt=""><figcaption></figcaption></figure>

Also check for "Security" and make sure the Group have it rights permissions

<div align="left"><figure><img src="../../.gitbook/assets/image (170).png" alt=""><figcaption></figcaption></figure></div>

## 2- Accessing the Shared Folder from the Client:

**For Windows 7 and Higher version :**

Open File Explorer, then navigate to Network. If you see this warning, click on it.

<div><figure><img src="../../.gitbook/assets/image (148).png" alt=""><figcaption></figcaption></figure> <figure><img src="../../.gitbook/assets/image (149).png" alt=""><figcaption></figcaption></figure></div>

Here you should enter any user inside the server who got admin privilege like `Tom` in our case or Server Administrator account

<figure><img src="../../.gitbook/assets/image (150).png" alt=""><figcaption></figcaption></figure>

If the Share Folder didn't show up you can try:

**Win + R** and write **`\\yourServerIP\ShareFolderName`**

<figure><img src="../../.gitbook/assets/image (164).png" alt=""><figcaption></figcaption></figure>

<details>

<summary>Windows XP Configuration</summary>

open Start menu ⇒ My computer ⇒ My Network Places ⇒ Add a Network Place

<div><figure><img src="../../.gitbook/assets/image (156).png" alt=""><figcaption></figcaption></figure> <figure><img src="../../.gitbook/assets/image (157).png" alt=""><figcaption></figcaption></figure></div>

Click on "Choose another network location then write `\\YourServerIP\SharedFolderName`

<div><figure><img src="../../.gitbook/assets/image (168).png" alt=""><figcaption></figcaption></figure> <figure><img src="../../.gitbook/assets/image (158).png" alt=""><figcaption></figcaption></figure></div>

<figure><img src="../../.gitbook/assets/image (159).png" alt=""><figcaption></figcaption></figure>

</details>

### Test sharing Permissions :

in the server I make this text file with this content

<figure><img src="../../.gitbook/assets/image (14) (1).png" alt=""><figcaption></figcaption></figure>

I make new user and add it to NetAdmin group that they have permissions for read only and I try to change the text :

<div><figure><img src="../../.gitbook/assets/image (15) (1).png" alt=""><figcaption></figcaption></figure> <figure><img src="../../.gitbook/assets/image (16) (1).png" alt=""><figcaption></figcaption></figure></div>

### Additional way for Windows 10

<details>

<summary>Enabling Network Discovery for Shared Folder Access in Windows 10</summary>

If you are using **Windows 10** and do not want to manually access (Win + R) to the shared folder every time, follow these steps:\
\
Search for **"Turn Windows features on or off"** then click on it

<figure><img src="../../.gitbook/assets/image (153).png" alt=""><figcaption></figcaption></figure>

Enter any user inside the server who got admin privilege if they ask

<figure><img src="../../.gitbook/assets/image (154).png" alt=""><figcaption></figcaption></figure>

Search for SMB 1.0/CIFS File Sharing Support and Make it on

<figure><img src="../../.gitbook/assets/image (155).png" alt=""><figcaption></figcaption></figure>

{% hint style="warning" %}
Note: SMB 1.0 was enabled for compatibility in this lab. However, it is insecure and should not be used in real environments due to known vulnerabilities and lack of modern security features
{% endhint %}

</details>
