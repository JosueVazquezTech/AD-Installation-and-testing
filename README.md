<p align="center">
  
![Image](https://github.com/user-attachments/assets/ad8da1a3-4fff-4af2-bd17-cdd14d39da67)


<h1> Deploying Active Directory, creating Admin Users and adding other computers to the domain</h1>
This guide outlines the process for installing  Active Directory and showing some use cases like group policy and account management. <br />




<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines)
- Remote Desktop/Bastion
- Active Directory Users and Computers 

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

We will create 2 new Organizational units for our regular employees and another one for admin users. To do this right-click on the domain, then click New, and then click Organizational Unit. We will name the first one **_EMPLOYEES** and click ok. Then we will repeat the process and create another OU and name it **_ADMINS**. 

![Image](https://github.com/user-attachments/assets/142392ea-3c89-40bd-b252-018ae1d33582)

![Image](https://github.com/user-attachments/assets/36d539ea-d9e9-428c-9f13-a21b5eb739ad)

![Image](https://github.com/user-attachments/assets/c95d1df1-2fde-4158-9715-5791a9fafe3f)

![Image](https://github.com/user-attachments/assets/0515a9cd-6aa1-4c38-b47c-a3642550878b)

Now we are gonna create a new Admin User, right-click in the _ADMINS OU we created, then click New, and then click User. Then you will be prompted to add a name, last name, and user login for this account. I choose Jane Doe as the name and last name and my user login will be **jane_admin**. Remember that to log into this account you will still have to add the domain context for the username, so when logging in the username should be **mydomain.com\jane_admin**. Click next and then type a new password for this account, in a normal work environment you might check "User must change password at next login" so the employee using this account can create their password but for this guide, we will leave it unchecked and click next. I created a se

![Image](https://github.com/user-attachments/assets/be3cdf5f-2f25-421e-bd02-2cd767b43015)

![Image](https://github.com/user-attachments/assets/85964598-bbaa-4855-8d8c-fafc99a66dcd)

![Image](https://github.com/user-attachments/assets/12e810e1-1ff0-4733-98fc-cd7a2b255ee4)

Now that we have a new user we can give it Domain Admin privileges, to do this right-click on the new user and click "Add to a group." On the pop-up window make sure that "From this location" is set to your domain name and on the text box write **Domain Admins** then click Check Names and OK. Now the Jane Doe account we created is also a Domain Admin. This will be our Domain Admin account from now on.

![Image](https://github.com/user-attachments/assets/d906cda6-0676-47bc-9139-bda379c9a114)

![Image](https://github.com/user-attachments/assets/a5dfdaee-f633-4388-8353-19a3bfbf8be3)

<h3> Join Client1 virtual machine to the domain and setup remote desktop access for non-administrative users on Client1</h3>

First, we will log into the Client1 virtual machine that we created at the beginning of this guide. Once we are logged in we will go to "Settings" and click About, under Related Settings we will click Rename this PC (advanced.) Then click Change... and under "Member of" you will check Domain and write your domain name on the text box. The reason we are able to do this is because previously we changed the DNS settings of Client1 to point to our Domain Controller, so when Client1 is looking up **mydomain.com** is getting directed to our server. After you click OK you will be prompted to enter the username and password of an account with permission to join the domain. Here we will use the Domain Admin account we just created, in my case is **mydomain.com\jane_admin**. Now the Client1 computer is part of our domain and we can login there as an Admin User. To test that everything we just did is working properly log back into DC1 virtual machine with the Jane Doe admin account, open Active Directory, and under the Computers OU you should see Client1 has joined.

![Image](https://github.com/user-attachments/assets/b2f4c423-b962-4e15-acb1-6f3fea127f0b)

![Image](https://github.com/user-attachments/assets/52dc29b2-e7ac-4a9e-9634-718fd001e5ff)

![Image](https://github.com/user-attachments/assets/d2e6b395-ee87-4790-ba1a-0211e95e3d14)

![Image](https://github.com/user-attachments/assets/82802563-f354-4d0c-9dd4-e973dbbdaddc)

<h3> Enabling Remote Desktop Connection</h3>


This will allow non admin users from the same domain to access Client1 computer remotely. To enable this go to the settings on your computer and then go to Remote Desktop or type "remote desktop" on the Windows search. After you get to the Remote Desktop window click on Advanced Options. Then, under User accounts click on "Select users that can remotely access this PC". In the pop-up window click add. On the new window make sure that the domain we created is listed under "from this location" and then under "Enter the object names to select" type "Domain Users" and click Check Names. You should see a new window listing the users that can access the computer remotely, click OK and you are all set up. Now anyone from our domain can access this computer remotely!


![Image](https://github.com/user-attachments/assets/a65d6924-670d-41c8-986e-fd8646dd8ea1)

![Image](https://github.com/user-attachments/assets/d2b2ff03-4303-4e17-b93c-7ab984098296)

![Image](https://github.com/user-attachments/assets/a219e708-5080-4779-b88d-2bf299473c39)

![Image](https://github.com/user-attachments/assets/a160ab71-981f-44b1-b4fb-b04aee4bd081)


![Image](https://github.com/user-attachments/assets/0279c3e8-a455-4b38-ba38-518e4946ad3f)






































