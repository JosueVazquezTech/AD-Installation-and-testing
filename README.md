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






