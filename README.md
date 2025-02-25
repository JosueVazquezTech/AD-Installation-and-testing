<p align="center">
  
![Image](https://github.com/user-attachments/assets/ad8da1a3-4fff-4af2-bd17-cdd14d39da67)


<h1> Deploying Active Directory, creating users and managing Group Policy</h1>
This guide outlines the process for installing  Active Directory and showing some use cases like group policy and account management. <br />




<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines)
- Remote Desktop/Bastion
- Active Directory Users and Computers
- Group Policy Management
- Event Viewer 

<h2>Operating Systems Used </h2>

- Windows 10 (21H2)
- Windows Server 2022 

<h2>High-Level Deployment and Configuration Steps</h2>

- Install Active Directory
- Create a Domain Admin user within the domain
- Join Client1 to the domain
- Setup Remote Desktop for non-admin users on Client1
- Group Policy and managing account
  
<h2>Setup and Configuration</h2>

<h3> Installing Active Directory</h3>

Welcome! This is the last step of my Active Directory guide that we are deploying within Microsoft Azure. For this final step, you should have already set up a Domain Controller virtual machine and a Client virtual machine and their corresponding DNS settings. If you have not done that yet, please refer to the previous steps [here](https://github.com/JosueVazquezTech) 

The first thing we are going to do is installing Active Directory in our DC virtual machine and promoting it to Domain Controller. Go to Azure and connect to our DC virtual machine, you should see the Server Manager Dashboard when you connect to it. Click "Add roles and features". After that you can use the default settings and click next until you get to "Server Roles", here "File and and Storage Services" should be already checked and you are also gonna check "Active Directory Domain Services" and click next. A small pop-up window should appear asking you to add the required features for Active Directory, click "Add Features". Then you can click next until you get to the "Results" page where you will have to wait for the installation (this might take a long time.)

![Image](https://github.com/user-attachments/assets/7cbca3ac-a5d8-46f5-84c8-ee1415afcd03)

![Image](https://github.com/user-attachments/assets/dea02a31-4c00-41c4-be3e-db8316427879)

![Image](https://github.com/user-attachments/assets/c28d2179-12d6-4dfd-81d0-1b529250c7ff)

![Image](https://github.com/user-attachments/assets/a03f61f4-e3c5-4628-a403-7a02a9ee7717)

Now it's time to promote our server to Domain Controller. Until now our VM has been a domain controller only in name, we don't have any of the functions of a Domain Controller. After promoting the server we will be able to Authorize, Authenticate accounts, and enforce Group Policies among other things. To do this, go to the Server Manager Dashboard, and on the top right corner you should see a flag letting you know that a configuration is required, open it and then click "promote this server to a domain controller". In the Deployment Configuration window check "add a new forest" and on the Root domain name we will create our domain, mine will be called **mydomain.com**. On the next page Domain Name System (DNS) server and Global Catalog (GC) should be checked by default. Here we will also create the password for our domain and then click next. On the DNS Options page leave "Create DNS delegation" unchecked and you can keep clicking next until you get to the Prerequisites Check. After all prerequisite checks have passed you should be able to click install. 

![Image](https://github.com/user-attachments/assets/c7d1e406-7db3-4346-b7f7-61aa2a00c097)

![Image](https://github.com/user-attachments/assets/c9021646-e598-45f0-a5ff-a2e076022438)

![Image](https://github.com/user-attachments/assets/cd841378-112a-40f6-87c8-9c61f2bb85e7)

![Image](https://github.com/user-attachments/assets/d53824ed-161a-4e70-aaf6-f871d42ed263)

![Image](https://github.com/user-attachments/assets/0ac52a39-51da-49b3-8d0d-29808aca82ee)

![Image](https://github.com/user-attachments/assets/a9bf7bfd-c493-46c0-b299-abee1135288f)

Now to make sure everything we did is working we have to logout and log back in, but instead of login into the local account we will log into the domain we just created. To do this in the login page when you are prompted to write your username you will write the domain name followed by a backslash followed by your username. It should look something like this: **mydomain.com\dclabuser**. After you log in you can go to the Settings page and go to "Your info" and you should see that you are logged into the domain as the Administrator. Now that we have Admin privileges we can create other Admin accounts, connect other computers to our domain, and many other useful things. 

![Image](https://github.com/user-attachments/assets/2eb857bb-7536-4c31-8812-350e49e8f095)

![Image](https://github.com/user-attachments/assets/2988d5a8-532a-41ed-8e02-eb00c76cd396)

<h3> Creating a Domain Admin user within the domain</h3>

Now we can start using Active Directory, you can find it a couple of different ways: you can open the "Run" app and type "dsa.msc", you can also find it in the Start Menu under Administrative tools or just search it in the windows search bar. Open Active Directory Users and Computers and you should see the domain we created followed by many other folders. These folders are called Organizational Units (OU), think of them as containers within our domain that we can use to organize and manage objects such as users, groups, and computers. You can also use the OUs to help apply policies to large groups of users, delegate administrative control, and maintain a structured hierarchy. 

We will create 2 new Organizational units for our regular employees and another one for admin users. To do this right click on the domain, then click New and then click Organizational Unit. We will name the first one **_EMPLOYEES** and click ok. Then we will repeat the process and create another OU and name it **_ADMINS**. 

![Image](https://github.com/user-attachments/assets/142392ea-3c89-40bd-b252-018ae1d33582)

![Image](https://github.com/user-attachments/assets/36d539ea-d9e9-428c-9f13-a21b5eb739ad)

![Image](https://github.com/user-attachments/assets/c95d1df1-2fde-4158-9715-5791a9fafe3f)

![Image](https://github.com/user-attachments/assets/0515a9cd-6aa1-4c38-b47c-a3642550878b)















