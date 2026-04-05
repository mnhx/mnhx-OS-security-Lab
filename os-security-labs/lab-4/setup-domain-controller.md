# Setup Domain Controller

After finish setup the windows server you will be in this page :&#x20;

### **Installing the AD DS role:**

<figure><img src="../../.gitbook/assets/image (51).png" alt=""><figcaption></figcaption></figure>

Select **Add roles and features then next**

<div><figure><img src="../../.gitbook/assets/image (52).png" alt="" width="563"><figcaption></figcaption></figure> <figure><img src="../../.gitbook/assets/image (54).png" alt=""><figcaption></figcaption></figure></div>

select Active Directory Domain Services in turn it will pop-up to add other\
active directory domain server related tools. Click on Add Features.

<figure><img src="../../.gitbook/assets/image (55).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (56).png" alt=""><figcaption></figcaption></figure>

make sure **Group Policy Management** is selected then press Next then next&#x20;

<figure><img src="../../.gitbook/assets/image (59).png" alt=""><figcaption></figcaption></figure>

After finish installing you will return to mean page and see warning sing on the flag click on it then click on **Promote this server to a domain controller**

<figure><img src="../../.gitbook/assets/image (60).png" alt=""><figcaption></figcaption></figure>

Select add new forest then enter the domain name

<figure><img src="../../.gitbook/assets/image (62).png" alt=""><figcaption></figcaption></figure>

Setup a password and as I mentioned before try to [store](pre-installation-preparation.md) it so you don't lose your work&#x20;

<figure><img src="../../.gitbook/assets/image (63).png" alt=""><figcaption></figcaption></figure>

<div><figure><img src="../../.gitbook/assets/image (32) (1).png" alt=""><figcaption></figcaption></figure> <figure><img src="../../.gitbook/assets/image (33) (1).png" alt=""><figcaption></figcaption></figure> <figure><img src="../../.gitbook/assets/image (34) (1).png" alt=""><figcaption></figcaption></figure></div>

Make sure you got the same script to void any errors

<figure><img src="../../.gitbook/assets/image (35).png" alt=""><figcaption></figcaption></figure>

<details>

<summary>Command :</summary>

Make sure to change the <mark style="color:$primary;">Domain name</mark> as yours and the <mark style="color:$warning;">Version</mark> if you use Newest one also if you did change any of the <mark style="color:green;">paths</mark> (I guess the command is useless (: )

```
# Windows PowerShell script for AD DS Deployment

Import-Module ADDSDeployment

Install-ADDSForest `
-CreateDnsDelegation:$false `
-DatabasePath "C:\Windows\NTDS" `
-DomainMode "Win2012R2" `
-DomainName "IAU_CYS.sa" `
-DomainNetbiosName "IAU_CYS" `
-ForestMode "Win2012R2" `
-InstallDns:$true `
-LogPath "C:\Windows\NTDS" `
-NoRebootOnCompletion:$false `
-SysvolPath "C:\Windows\SYSVOL" `
-Force:$true
```

</details>

Install then let system do reboot

<figure><img src="../../.gitbook/assets/image (36).png" alt=""><figcaption></figcaption></figure>

After Reboot and open the Server Manager click on Tools

<figure><img src="../../.gitbook/assets/image (37).png" alt=""><figcaption></figcaption></figure>

if you have this 6 Features you done 👍



### Common errors: <a href="#common-errors" id="common-errors"></a>

<figure><img src="../../.gitbook/assets/image (87).png" alt=""><figcaption></figcaption></figure>

Click on the Services&#x20;

then click in each one and press Start Services

<figure><img src="../../.gitbook/assets/image (88).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (89).png" alt=""><figcaption></figcaption></figure>
