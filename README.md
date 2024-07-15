<p align="center">
<img src="https://i.imgur.com/pU5A58S.png" alt="Microsoft Active Directory Logo"/>
</p>

<h1>Active Directory Deployed in the Cloud (Azure)</h1>
This tutorial outlines the implementation of Active Directory within Azure Virtual Machines.<br />


<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Active Directory Domain Services
- PowerShell

<h2>Operating Systems Used </h2>

- Windows Server 2022
- Windows 10 Pro

<h2>High-Level Deployment and Configuration Steps</h2>

- Setting Resources in Azure
- Ensure Connectivity between the client and domain controller
- Install Active Directory
- Create an Admin and Normal User Account in AD
- Join Client-1 to your domain (mydomain.com)
- Create additional users and attempt to log into client-1 with one of the users

<h2>Setting Resources in Azure</h2>

- Create first virtual machine (Windows server 2022) named "DC-1". Observations: Use same region. Use 2 virtual CPUs.

![Screenshot 2024-07-07 172355](https://github.com/user-attachments/assets/0f71e532-c295-462a-b773-5aeba5ef039f)
![Screenshot 2024-07-07 172445](https://github.com/user-attachments/assets/49fda395-01e3-4cc0-8aaa-163bfe49592c)
![Screenshot 2024-07-07 172500](https://github.com/user-attachments/assets/1c76a39d-c4bb-4ba5-81f4-80883a758245)
![Screenshot 2024-07-07 172510](https://github.com/user-attachments/assets/e5d51593-88fa-4788-bccc-21cc08515dc8)
![Screenshot 2024-07-07 172522](https://github.com/user-attachments/assets/a057474c-4b88-4b1d-b7b5-1dc90a4e4f56)
![Screenshot 2024-07-07 172649](https://github.com/user-attachments/assets/e60b3b4e-41ce-4144-ae12-47665cd003eb)
![Screenshot 2024-07-07 172829](https://github.com/user-attachments/assets/f84b819a-3797-438a-a0fe-f7779a5189e5)
![Screenshot 2024-07-07 172923](https://github.com/user-attachments/assets/ab1589e5-807c-4bb5-adef-8f3da8ab2999)

- Set Domain Controller NIC IP Address to static. 

![Screenshot 2024-07-07 173213](https://github.com/user-attachments/assets/9bd55293-7d05-4c52-8912-1929e484e722)
![Screenshot 2024-07-07 173225](https://github.com/user-attachments/assets/18336070-ad88-4f9d-9cf9-b038450a0b5e)
![Screenshot 2024-07-07 173311](https://github.com/user-attachments/assets/0930b79e-ad0a-4fde-a3b6-36d71ca0f961)
![Screenshot 2024-07-07 173326](https://github.com/user-attachments/assets/ed5bbb5e-f324-4718-b7a7-d915d7aa7cf9)
![Screenshot 2024-07-07 173400](https://github.com/user-attachments/assets/dd89f757-251c-40dc-a204-ac96f76e7f6f)
![Screenshot 2024-07-07 173412](https://github.com/user-attachments/assets/f60fe0f5-c7f0-40ff-8583-98d9abefa7b4)


- Create second virtual machine (Windows 10 Pro) named "Client-1". Observations: Place virtual machine in the same resource group as DC-1. Make sure the virtual network is the same as the domain controller (DC-1).

![Screenshot 2024-07-07 173456](https://github.com/user-attachments/assets/a436d8e9-695c-495e-a642-301a9bfaf938)
![Screenshot 2024-07-07 173533](https://github.com/user-attachments/assets/f7a8a3e3-e524-4bd8-9128-0cd75a5737ca)
![Screenshot 2024-07-07 173712](https://github.com/user-attachments/assets/d8994bba-f781-4efe-9a26-e34c36733c26)
![Screenshot 2024-07-07 174009](https://github.com/user-attachments/assets/30404566-c606-4cd2-b4ae-8f1a27b49994)
![Screenshot 2024-07-07 174049](https://github.com/user-attachments/assets/b5f459a7-7f7d-4560-a4d6-132921e04d67)
![Screenshot 2024-07-07 174635](https://github.com/user-attachments/assets/c5ac87e0-a177-441a-8f42-575f3d95b097)
![Screenshot 2024-07-07 174757](https://github.com/user-attachments/assets/63b321ee-33b9-4cb0-8182-a7aac6bb298f)
![Screenshot 2024-07-07 174812](https://github.com/user-attachments/assets/6f5c75d8-09d4-487c-81c9-9dbdf76f7fc6)

<h2>Ensure Connectivity between the client and domain controller</h2>

- Login to Client-1 with Remote Desktop and ping DC-1 private IP Address.










 








