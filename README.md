<p align="center">
<img src="https://github.com/user-attachments/assets/69f8252a-00a3-484a-b9f0-66c84c54adc4"/>
</p>

<h1>Configuring Network File Shares and Permissions within Azure</h1>
This tutorial outlines the implementation of file sharing and permission settings within Azure Virtual Machines.<br />

<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Active Directory Domain Services

<h2>Operating Systems Used </h2>

- Windows Server 2022
- Windows 10 (22H2)

<h2>High-Level Deployment and Configuration Steps</h2>

- Create some sample file shares with various permissions
- Attempt to access file shares as a normal user
- Create an “ACCOUNTANTS” Security Group, assign permissions, and test access

<h2>Deployment and Configuration Steps</h2>  

<p>
<img src="https://github.com/user-attachments/assets/0872cdee-5318-454a-8a42-964dbb9d787f" height="50%" width="50%"/>
</p>
<p>
This is a continuation of the Active Directory project. Open Active Directory Users and Computers on DC-1 and pick a user to log into Client-1 with. Remember the passwords created for the users were "Password1".
</p>
<br />

<p>
<img src="https://github.com/user-attachments/assets/ca21b87a-f43e-4a66-afd5-23f458ff47fd" height="50%" width="50%"/>
</p>
<p>
After logging into Client-1 with the random user, go to DC-1's File Explorer. We are going to create four new folders. We'll call them "read-access", "write-access", "no-access" and "accountants".
</p>
<br />

<p>
<img src="https://github.com/user-attachments/assets/43b8fc00-37ad-4b4c-95ec-30117e8e8569" height="50%" width="50%"/>
</p>
<p>
For "read-access", go to properties, then sharing and click "share". Add Domain Users and make sure the permission is on "Read".
</p>
<br />

<p>
<img src="https://github.com/user-attachments/assets/841f2234-5590-43a2-afd0-32ce76976a32" height="50%" width="50%"/>
</p>
<p>
For "write-access", go to properties, then sharing and click "share". Add Domain Users and make sure the permission is on "Read/Write".
</p>
<br />

<p>
<img src="https://github.com/user-attachments/assets/46f1c2ef-f6e8-483d-b713-8aa5db681efd" height="50%" width="50%"/>
</p>
<p>
For "no-access", go to properties, then sharing and click "share". Add Domain Admins and make sure the permission is on "Read/Write". We are adding Domain Admins this time instead of Domain Users because normal users should not be able to access it.
</p>
<br />

<p>
<img src="https://github.com/user-attachments/assets/c60a7b40-2951-4f0a-8c85-c372f25b31b7" height="50%" width="50%"/>
</p>
<p>
Go to Client-1 now and open File Explorer. In the search, enter the file path we just created on DC-1. The path is \\dc-1. Notice how now we have the files on Client-1.
</p>
<br />

<p>
<img src="https://github.com/user-attachments/assets/c72dc13e-2226-4f27-9b2d-d6c7ae530df1" height="50%" width="50%"/>
</p>
<p>
Since we only have read access for the "read-access" folder, we cannot write anything to it. 
</p>
<br />


<p>
<img src="https://github.com/user-attachments/assets/5595f23f-b200-4ee0-80ea-369d970ae9fd" height="50%" width="50%"/>
</p>
<p>
We have write access to the "write-access" folder, so I was able to create a sample text document.
</p>
<br />

<p>
<img src="https://github.com/user-attachments/assets/8ddef462-bbda-4aaf-8fa2-03e689c60a53" height="50%" width="50%"/>
</p>
<p>
We have no access to the "no-access" folder. 
</p>
<br />

<p>
<img src="https://github.com/user-attachments/assets/87986f49-b1e9-4411-bdc4-147090bc8865" height="50%" width="50%"/>
</p>
<p>
I created a text document on DC-1 to demonstrate how we can only read it on Client-1, but cant write to it.
</p>
<br />

<p>
<img src="https://github.com/user-attachments/assets/d4e2cce3-1638-4974-a4aa-1ce223c726e0" height="50%" width="50%"/>
</p>
<p>
We are now going to assign permissions to the "accountants" folder we created earlier. First I am going to created a new Organizational Unit in Active Directory called _SECURITY_GROUPS. In _SECURITY_GROUPS, we are going to create a Security Group called "ACCOUNTANTS".
</p>
<br />

<p>
<img src="https://github.com/user-attachments/assets/5a325e8a-b13a-478b-8578-d11c647064b9" height="50%" width="50%"/>
</p>
<p>
Go back to File Explorer and under the accounting folder we made select properties. Under sharing, click Share and add the ACCOUNTANTS Security Group we just made. Make sure the permission level is Read/Write.
</p>
<br />

<p>
<img src="https://github.com/user-attachments/assets/94f11211-efca-455d-9887-d212b67d5683" height="50%" width="50%"/>
</p>
<p>
We will now give Client-1 access to the accountants folder. In Active Directory, go to the _SECURITY_GROUPS we created and open the ACCOUNTANTS Group. Select "Members" and right now it is empty. Click "Add" and enter the username we selected earlier. Click OK. 
</p>
<br />

<p>
<img src="https://github.com/user-attachments/assets/93484547-ddd8-4509-b89b-dabeceb41623" height="50%" width="50%"/>
</p>
<p>
Log off of Client-1 and log back in as the same user. We now have access to the accountant's folder.
</p>
<br />







































