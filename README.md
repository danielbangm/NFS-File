<p align="center">
<img src="https://rb.gy/z4mg2" />
</p>

<h1>Network File Shares and Permissions: Creating sample File Shares with various Permissions</h1>

In this lab I am going to be sharing files and folders essentially on the network and kinda allowing different group of people to have different level of access

<h2>Objectives</h2>

-  More Experience with Azure (I will Create the environment here)
-  Create and test some file shares
-  Create and test Security Groups
-  Gain a better understanding of File Sharing System.

<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Virtual Machine(DC-1)
- Virtual Machine(client-1)
- Remote Desktop
- Active Directory

<h2>Operating Systems Used</h2>

-  Windows Server 2022
-  Windows 10 pro

<h2>List of Prerequisites</h2>

-  All you need for this lab is the free Azure Tenant and Subscription and complete the previous <a href="https://github.com/danielbangm/Users-ad">Lab. </a>

<h2>Installation steps</h2>

-  Step 1: Create some sample file shares with various permissions 

I connect/log into DC-1 as domain admin account (mydomain.com\jane_admin) and Connect/log into Client-1 as a normal user (mydomain\babixi.fesuji). On DC-1, on the C:\ drive, I create 4 folders: “read-access”, “write-access”, “no-access”, “accounting”. I Set the following permissions (share the folder) for the “Domain Users” group:
Folder: “read-access”, Group: “Domain Users”, Permission: “Read”
Folder: “write-access”,  Group: “Domain Users”, Permissions: “Read/Write”
Folder: “no-access”, Group: “Domain Admins”, “Permissions: “Read/Write”
![image](https://github.com/danielbangm/NFS-File/assets/22795502/ff965b23-9f96-4fe6-99d3-60449a71001b)

To Share a file(assign permissions), just right click on the file and go to properties -> Sharing

-  Step 2: Attempt to access file shares as a normal user

I log/connect into Client-1, navigate to the shared folder (start, run, \\dc-1) trying to access the folders you just created. I notice that I can't have access to the "no-access" file; I can access the "read-access" and "write-access" files but cannot create anything in the "read-access" one. I can create stuff in the "write access" file. It makes perfect sense now!!!!!!!!
![image](https://github.com/danielbangm/NFS-File/assets/22795502/8b9c79d8-f99f-4b23-ba05-34d0b3b0063c)
![image](https://github.com/danielbangm/NFS-File/assets/22795502/08b15eec-50fa-4838-bbce-bcb6ba84a9a3)
![image](https://github.com/danielbangm/NFS-File/assets/22795502/399776bd-4700-4752-a086-356287f0fefd)

-  Step 3: Create an “ACCOUNTANTS” Security Group, assign permissions, an test access

I go back to DC-1, in Active Directory, create a security group called “ACCOUNTANTS” and then On the “accounting” folder created earlier, I set the following permissions: Folder: “accounting”, Group: “ACCOUNTANTS”, Permissions: “Read/Write”. On Client-1, as normal user <babixi.fesuji>, I try to access the accountants folder. It fails because this user is not a member od "ACCOUNTANTS" group
![image](https://github.com/danielbangm/NFS-File/assets/22795502/7447d4d5-b205-4ead-8381-90b74b5718bb)

In order to have acces to the "accounting" file/folder, we have to make <babixi.fesuji> a member of ACCOUNTANTS" group. I go back to DC-1 and add our user as a member of "ACCOUNTANTS" group. As I log back in Client-1 I am now able to access the "accounting" file
![image](https://github.com/danielbangm/NFS-File/assets/22795502/a04ece79-3ccc-4f42-b4fb-0a49a07088bd)

