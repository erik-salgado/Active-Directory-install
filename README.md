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

- Login to Client-1 with Remote Desktop and do a perpectual ping DC-1 private IP Address.

![Screenshot 2024-07-16 185544](https://github.com/user-attachments/assets/0ae815df-fc62-43a0-8e32-10378885cfa2)

Observations: If you notice the ping is timing out, that's because ICMP (Internet Control Message Protocol) is being blocked by DC-1 firewall. 
![Screenshot 2024-07-16 185720](https://github.com/user-attachments/assets/646300ca-0d50-488f-8d3a-2bc11e2f27dc)


- Go to DC-1 firewall and enable ICMP.

![Screenshot 2024-07-16 190218](https://github.com/user-attachments/assets/8022fcf5-08a2-4225-8109-bcff2e38452d)
![Screenshot 2024-07-16 190256](https://github.com/user-attachments/assets/6a3b2f26-f809-4f39-a9e6-cdc7dd602f2d)

Observations: Go back to Client-1 and connection should be established as a result of enabling ICMP.
![Screenshot 2024-07-16 190321](https://github.com/user-attachments/assets/847f121c-d8c2-4992-b3c1-1cd7f6c66ceb)

<h2>Install Active Directory</h2>

- Log in to DC-1 and on the Service Manager, select add roles and features.

![Screenshot 2024-07-07 181650](https://github.com/user-attachments/assets/42c7002f-f451-491f-83fc-1e1a94f445f7)
![Screenshot 2024-07-07 181711](https://github.com/user-attachments/assets/dd5bbc2d-7449-46e6-98db-576c88663483)
![Screenshot 2024-07-07 181726](https://github.com/user-attachments/assets/53f00829-a376-4961-b1e5-362fa5349474)
![Screenshot 2024-07-07 181736](https://github.com/user-attachments/assets/d5aedd9b-0623-4b5d-bd08-0a4e9142a410)
![Screenshot 2024-07-07 181842](https://github.com/user-attachments/assets/85177995-8788-4f0c-9639-5f8a1f0c4168)
![Screenshot 2024-07-07 181942](https://github.com/user-attachments/assets/0dfa025a-8c32-4109-885a-ef047850714d)
![Screenshot 2024-07-07 182046](https://github.com/user-attachments/assets/de29b9d2-e739-4fe7-9684-163cb203b52f)
![Screenshot 2024-07-07 182056](https://github.com/user-attachments/assets/e5f7b4cd-d5f0-4ff9-91fa-13019c3fa211)
![Screenshot 2024-07-07 182106](https://github.com/user-attachments/assets/0e213ef0-4d39-475a-8292-c6d48df46e97)
![Screenshot 2024-07-07 182300](https://github.com/user-attachments/assets/a9eb454c-c4dc-4f54-8cae-64bcc395db44)
![Screenshot 2024-07-07 182320](https://github.com/user-attachments/assets/46295291-13df-4aaa-8b84-bfc83913683c)
![Screenshot 2024-07-07 182400](https://github.com/user-attachments/assets/11692f28-c302-4e76-b34e-d6c90d46dd47)
![Screenshot 2024-07-07 182511](https://github.com/user-attachments/assets/558b0b74-afbd-46af-99ad-c7b99b5be598)
![Screenshot 2024-07-07 182704](https://github.com/user-attachments/assets/5690f2da-3196-481d-b019-2f91e3f87b3b)
![Screenshot 2024-07-07 182751](https://github.com/user-attachments/assets/0cc99a2b-6263-40b0-abed-faac68de729e)
![Screenshot 2024-07-07 182848](https://github.com/user-attachments/assets/be20242a-495a-4fb8-bc13-cc911c524a45)
![Screenshot 2024-07-07 182917](https://github.com/user-attachments/assets/20802058-fe57-4ac7-b98a-18066d5a658d)
![Screenshot 2024-07-07 183105](https://github.com/user-attachments/assets/d2e76e93-da8c-44c1-b37c-8c1e97087818)
![Screenshot 2024-07-07 183246](https://github.com/user-attachments/assets/600e88ed-149e-4d0f-8cc1-5eba6b5dac01)
![Screenshot 2024-07-07 183812](https://github.com/user-attachments/assets/dcd38aa0-aadb-4615-bcb3-5cc7e6d4198d)
![Screenshot 2024-07-07 183830](https://github.com/user-attachments/assets/022bba9c-a3b7-4b87-8260-04ba3ea3e56a)

<h2>Create an Admin and Normal User Account in AD</h2>

- Select your domain (mydomain) on AD and select new organizational unit, name one "_EMPLOYESS" and another named "_ADMINS"

![Screenshot 2024-07-07 183852](https://github.com/user-attachments/assets/3b882419-f158-4c7f-8024-0c7abc354673)
![Screenshot 2024-07-07 183920](https://github.com/user-attachments/assets/0e575587-11f5-4300-813a-62eababc354a)
![Screenshot 2024-07-07 183934](https://github.com/user-attachments/assets/aaf38b98-37e8-41d8-86eb-f831c8b8fad3)
![Screenshot 2024-07-07 183959](https://github.com/user-attachments/assets/3568f58a-9d0b-44c7-b976-676e6a95b148)
![Screenshot 2024-07-07 184015](https://github.com/user-attachments/assets/eb0e8831-2d4d-4564-915d-45057f6071cd)
![Screenshot 2024-07-07 184033](https://github.com/user-attachments/assets/481fb58a-4359-44f1-8aea-d3b30453f303)
![Screenshot 2024-07-07 184043](https://github.com/user-attachments/assets/20bd4010-4d96-4536-9bdb-165dd0a85462)

- Go to "_ADMINS" organizational unit and select new user, name it "Jane Doe"

![Screenshot 2024-07-07 184148](https://github.com/user-attachments/assets/d1d23124-fb73-4126-b7d4-bc4d7d176ae0)
![Screenshot 2024-07-07 184320](https://github.com/user-attachments/assets/f3fb9be6-2630-4169-966e-dd68a68c01b0)
![Screenshot 2024-07-07 184454](https://github.com/user-attachments/assets/7a72e52b-f83a-4376-ad8c-5662f1bff645)
![Screenshot 2024-07-07 184541](https://github.com/user-attachments/assets/5950c2ca-ec81-4db5-903e-e4e7a7dc2627)

Observations: The account we created is not yet admin. To make this an actual domain admin, we need to assign it to the domain admins group.
![Screenshot 2024-07-07 184613](https://github.com/user-attachments/assets/ad236523-c89a-4be7-a663-d0bc8a16ce06)
![Screenshot 2024-07-07 184633](https://github.com/user-attachments/assets/e0a0a021-ca06-49b2-bdda-49fd579ca71b)
![Screenshot 2024-07-07 184703](https://github.com/user-attachments/assets/7b98a0e2-ae25-40ff-a92c-0f538cdd9d09)
![Screenshot 2024-07-07 184703](https://github.com/user-attachments/assets/60515368-bbcd-4673-8aea-45ccc73cb745)
![Screenshot 2024-07-07 184722](https://github.com/user-attachments/assets/787bf277-e444-47e0-a9d1-4da40d47425b)

- Log out of DC-1 and log in as your admin account "jane_admin"

![Screenshot 2024-07-07 184904](https://github.com/user-attachments/assets/a6646acf-6d84-4f16-aadc-5afd8707607f)

<h2>Join Client-1 to your domain (mydomain.com)</h2>

- From the Azure portal, set Client-1 DNS Settings to the DC-1 Private IP Address. Observations/Notes: We don't want Client-1 DNS to be something random from the internet. In order for Client-1 to be able to join the domain, it needs to use the domain controller as its DNS Server. *If you receive a error message from your browser when trying to change the DNS, restart your computer and try again.*

![Screenshot 2024-07-07 185817](https://github.com/user-attachments/assets/7af366f2-7124-4ee9-9f27-36382da5568f)
![Screenshot 2024-07-07 185829](https://github.com/user-attachments/assets/087304ed-58bc-4af3-a764-85a06b978a82)
![Screenshot 2024-07-07 185849](https://github.com/user-attachments/assets/741eb4a0-770b-4697-9f95-2fbd6db89659)
![Screenshot 2024-07-07 192438](https://github.com/user-attachments/assets/4ba9d0f8-4d82-4e68-8961-a03f78fa210f)
![Screenshot 2024-07-07 192512](https://github.com/user-attachments/assets/0e93b914-a83f-4693-b303-5d860b34f9ba)

- Restart Client-1 from the Azure Portal and Log back in as the original local admin (labuser)

![Screenshot 2024-07-16 203040](https://github.com/user-attachments/assets/3e46981e-22c3-41fc-95a9-3d548b1178a0)
![Screenshot 2024-07-16 200616](https://github.com/user-attachments/assets/0a69ef72-a362-411b-87cb-56611bc20c1c)
![Screenshot 2024-07-16 200700](https://github.com/user-attachments/assets/79d4f7db-a32c-465c-9acf-0068015a88da)
![Screenshot 2024-07-16 200739](https://github.com/user-attachments/assets/f886fb43-cc60-4b8c-b729-b9a592d7a161)
![Screenshot 2024-07-16 201647](https://github.com/user-attachments/assets/db84d012-2bf9-4b83-8426-ea011215400d)
![Screenshot 2024-07-16 203421](https://github.com/user-attachments/assets/439e02d3-956d-4912-92b3-ff10d4107a6e)
![Screenshot 2024-07-16 203524](https://github.com/user-attachments/assets/f3c341a3-5a1c-4264-ad49-2385ff90da4b)
![Screenshot 2024-07-16 203931](https://github.com/user-attachments/assets/ad05125e-fb88-4909-8a4e-efec2eb976f4)
![Screenshot 2024-07-16 203938](https://github.com/user-attachments/assets/3536e002-032a-46c5-b812-f1903a407044)
![Screenshot 2024-07-16 203950](https://github.com/user-attachments/assets/1ab20918-7265-4aef-985d-71de2b2a7f28)

- Log back in to Client-1 as "mydomain.com\jane_admin" and set up so that normal users are able to remote into Client-1

![Screenshot 2024-07-07 184904](https://github.com/user-attachments/assets/190cb2f4-0b9a-4667-9b9e-acd570e08991)
![Annotation 2024-07-10 002817](https://github.com/user-attachments/assets/e4f49c02-b4ba-46c4-a71b-34bf589c619c)
![Annotation 2024-07-10 002930](https://github.com/user-attachments/assets/ee2a7fc9-44e4-480a-b4e6-0b9684d79a87)
![Annotation 2024-07-10 003041](https://github.com/user-attachments/assets/ba5e2d8a-2111-4e05-a166-7787898055eb)
![Annotation 2024-07-10 003114](https://github.com/user-attachments/assets/6085de5e-4651-4ce2-98e5-e4312c0f6983)
![Annotation 2024-07-10 003138](https://github.com/user-attachments/assets/42b15f4f-29f5-4efb-aecc-d300ecfd1ba0)

- Go to Active Directory and select the users under your domain name (mydomain). Observations: Notice that all the users can now log in to Client-1

![Screenshot 2024-07-16 210031](https://github.com/user-attachments/assets/613d2b62-2c07-4298-a11d-f8c40bcf5bf6)

<h2>Create additional users and log into Client-1 with one of the users</h2>

- Log in to DC-1 as "jane_admin"

![Screenshot 2024-07-07 184904](https://github.com/user-attachments/assets/af2380f1-c9bf-4228-8e4a-40da14514a1e)

- Open Powershell ISE as an administrator (Powershell ISE is a native scriptive language)

![Screenshot 2024-07-09 194424](https://github.com/user-attachments/assets/65275b76-704a-45fe-b1c8-baf480c3fb54)

- Select New Script

![Screenshot 2024-07-09 194617](https://github.com/user-attachments/assets/4099c19f-55ed-49c5-b57b-f1ecbb061f6c)

- Copy code and paste it in Powershell ISE (https://github.com/joshmadakor1/AD_PS/blob/master/Generate-Names-Create-Users.ps1)

![Screenshot 2024-07-18 194244](https://github.com/user-attachments/assets/f24db28c-3b3c-419e-ab87-13d13b29e8cd)
![Screenshot 2024-07-09 194834](https://github.com/user-attachments/assets/727ad36b-e29e-4253-9fe2-d22cab5f154d)

- Run script

![Screenshot 2024-07-09 194851](https://github.com/user-attachments/assets/1093c07b-ef99-4034-aa22-a06fdf68eff9)

The script will run and will create our users.
![Screenshot 2024-07-09 194908](https://github.com/user-attachments/assets/63995ea7-b5fc-43b1-aee7-c2a1e79b7254)

- Go to Active Directory > mydomain.com > _EMPLOYESS.

As you can see here we have created our users. This are all random names. 
![Screenshot 2024-07-09 194958](https://github.com/user-attachments/assets/d91486b2-d2a0-4240-bd9e-e8679c35cd14)

I'm going to use one random name and log in as that user. For the sake of this lab I will purposely type the wrong password as many times as possible. I will then unlock the users account as an admin.
![Screenshot 2024-07-09 195056](https://github.com/user-attachments/assets/0faef9af-6bec-4d7f-b98c-304ae058d922)

I chose this random user. Make sure to remember the name when trying to unlock the account.
![Screenshot 2024-07-09 195106](https://github.com/user-attachments/assets/75557e96-9e60-4562-93fb-eba6a86fb7e1)

At this point I have type the wrong password for more than 10 times. Account should be locked by now.
![Screenshot 2024-07-09 195734](https://github.com/user-attachments/assets/f1243e8c-7962-4db7-9f32-9b6988e043ff)

Go to DC-1 Active Directory and unlock the users account. The user will now be able to log in. There is also the option to change password if the user have forgotten his/her password.
![Screenshot 2024-07-09 195907](https://github.com/user-attachments/assets/afac9602-5fbf-43ae-8b8d-bf1ede420e16)

This brings us the conclusion for this Lab. Thank you for watching! :)




















































































 








