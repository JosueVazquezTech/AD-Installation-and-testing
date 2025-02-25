<p align="center">
  
![Image](https://github.com/user-attachments/assets/ad8da1a3-4fff-4af2-bd17-cdd14d39da67)


<h1> Deploying Active Directory and testing some functions</h1>
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

Now it's time to promote our server to Domain Controller. Until now our VM has been a domain controller only in name, we don't have any of the functions of a Domain Controller. After promoting the server we will be able to Authorize, Authenticate accounts, and enforce Group Policies among other things. To do this, go to the Server Manager Dashboard, and on the top right corner you should see a flag letting you know that a configuration is required, open it and then click "promote this server to a domain controller". In the Deployment Configuration window check "add a new forest" and on the Root domain name we will create our domain, mine will be called "mydomain.com




