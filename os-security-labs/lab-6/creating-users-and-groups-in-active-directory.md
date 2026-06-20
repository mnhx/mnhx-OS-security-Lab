# Creating Users & Groups in Active Directory

This section covers the creation of user accounts and security groups in Active Directory.

Users are created with different roles and permissions, then organised into groups to simplify access management. Instead of assigning permissions to individual users, permissions are assigned to groups, and users inherit access based on group membership.\
\
for this this lab my admin account will be `Tom` and my individual account will be `Jerry`.

## 1- Creating Users

Open Server Manager Dashboard click on **tools** ⇒ **Active Directory Users and Computers**

<figure><img src="../../.gitbook/assets/image (144).png" alt=""><figcaption></figcaption></figure>

Then click right on Users ⇒ New ⇒ User

<figure><img src="../../.gitbook/assets/image (133).png" alt=""><figcaption></figcaption></figure>

Chose a name and user name and set password and write it store it somewhere

<div><figure><img src="../../.gitbook/assets/image (11).png" alt="" width="563"><figcaption></figcaption></figure> <figure><img src="../../.gitbook/assets/image (42).png" alt=""><figcaption></figcaption></figure> <figure><img src="../../.gitbook/assets/image.png" alt="" width="563"><figcaption></figcaption></figure></div>

We need to create another user with the option “User must change password at next logon”.

<div><figure><img src="../../.gitbook/assets/image (49).png" alt="" width="563"><figcaption></figcaption></figure> <figure><img src="../../.gitbook/assets/image (138).png" alt=""><figcaption></figcaption></figure></div>

### Testing Login After Creating Users

Click on “Log in with another account” and ensure that the domain is specified.\
If it is not displayed, manually enter it using the following format:

DomainName\Username

<div><figure><img src="../../.gitbook/assets/image (57).png" alt=""><figcaption></figcaption></figure> <figure><img src="../../.gitbook/assets/image (58).png" alt=""><figcaption></figcaption></figure></div>

### 2- Creating Groups

Right on Users ⇒ New ⇒ Group

<div><figure><img src="../../.gitbook/assets/image (20) (1).png" alt=""><figcaption></figcaption></figure> <figure><img src="../../.gitbook/assets/image (19) (1).png" alt=""><figcaption></figcaption></figure></div>

### adding members in the Group

you have 2 way to add member in group:

first way:\
Double click on the group ⇒ Members ⇒ Add

<div><figure><img src="../../.gitbook/assets/image (22) (1).png" alt=""><figcaption></figcaption></figure> <figure><img src="../../.gitbook/assets/image (21) (1).png" alt=""><figcaption></figcaption></figure></div>

Write the user name then click on "Check Names"

<div><figure><img src="../../.gitbook/assets/image (61).png" alt=""><figcaption></figcaption></figure> <figure><img src="../../.gitbook/assets/image (69).png" alt=""><figcaption></figcaption></figure></div>

Second way :\
\
Double click on your user ⇒ Members of ⇒ Add

Enter the group name then click on "Check Names"

<div><figure><img src="../../.gitbook/assets/image (85).png" alt="" width="375"><figcaption></figcaption></figure> <figure><img src="../../.gitbook/assets/image (26) (1).png" alt=""><figcaption></figcaption></figure></div>

### In addition your admin account should be member of these groups

\
Administrators\
Domain Admins\
Domain Users\
Schema Admins

<figure><img src="../../.gitbook/assets/image (94).png" alt="" width="563"><figcaption></figcaption></figure>
