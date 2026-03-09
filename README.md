<p align="center">
<img src="https://i.imgur.com/pU5A58S.png" alt="Microsoft Active Directory Logo"/>
</p>

<h1>Active Directory Deployment on Azure </h1>
This repository contains instructions and configurations for deploying an on-premises Active Directory environment on Azure Virtual Machines. The steps outlined in this repository demonstrate the setup and management of Active Directory Domain Services within a cloud-based environment.<br />


<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Active Directory Domain Services
- PowerShell

<h2>Operating Systems Used </h2>

- Windows Server 2022
- Windows 10 (21H2)


<h2>Deployment and Configuration Steps</h2>

*1. Install Active Directory*
---
### Login to DC-1
Connect to the **DC-1 Virtual Machine** using Remote Desktop.

**Credentials**

* **Username:** `Administrator`
* **Password:** `your password`

### Install Active Directory Domain Services
1. Open **Server Manager**.
2. Click **Add Roles and Features**.
3. Select **Active Directory Domain Services (AD DS)**.
4. Complete the installation.

<img width="1089" height="824" alt="Screenshot 2026-03-02 210042" src="https://github.com/user-attachments/assets/741bf009-c986-4762-92f0-d8042f40d685" />
<img width="423" height="333" alt="Screenshot 2026-03-02 210652" src="https://github.com/user-attachments/assets/f01b3a70-1bec-46b8-9ed6-68d867feb75a" />

### Promote Server to Domain Controller
1. In **Server Manager**, click the **notification flag**.
2. Select **Promote this server to a domain controller**.
3. Choose **Add a new forest**.
4. Enter the domain name:
   
```
mydomain.com
```

5. Complete the setup and allow the server to **restart**.

<img width="750" height="551" alt="Screenshot 2026-03-02 210910" src="https://github.com/user-attachments/assets/121eae31-5dd7-41e7-8761-58deb334139a" />

### Login Using Domain Account
After the restart, log back into `DC-1`.

* **Username:** `mydomain.com\Administrator`
* **Password:** `your password`

*2. Create a Domain Admin User*
---
### Open Active Directory Users and Computers
On `DC-1`, open `Active Directory Users and Computers (ADUC)`.

### Create Organizational Units
Create two Organizational Units (OUs):
* `_EMPLOYEES`
* `_ADMINS`

<img width="432" height="366" alt="Screenshot 2026-03-02 212943" src="https://github.com/user-attachments/assets/b8502dfb-d252-4a61-b087-c438874e0a2e" />
<img width="429" height="370" alt="Screenshot 2026-03-02 213020" src="https://github.com/user-attachments/assets/c3c27f7d-424a-424b-8e16-1249fb91ccfe" />

### Create a New User

Create a user with the following details:
* **Name:** `Jane Doe`
* **Username:** `jane_admin`
* **Password:** `your password`

Place the user in the `_ADMINS` OU.

### Add User to Domain Admins
Add `jane_admin` to the **Domain Admins** security group.

<img width="569" height="476" alt="Screenshot 2026-03-02 213255" src="https://github.com/user-attachments/assets/495b7b62-10c5-478a-a914-c7d0541929b1" />
<img width="432" height="371" alt="Screenshot 2026-03-02 213358" src="https://github.com/user-attachments/assets/59552757-16a5-43b5-a4c8-9244fa86ab4c" />
<img width="498" height="355" alt="Screenshot 2026-03-02 213609" src="https://github.com/user-attachments/assets/4f860ebd-ddef-4ca6-8a33-111132a85fe6" />


### Log in as jane_admin
Log out of `DC-1` and log back in using:

* **Username:** `mydomain.com\jane_admin`
* **Password:** `your password`

Use **jane_admin** as the admin account for the rest of the lab.

<img width="442" height="315" alt="Screenshot 2026-03-02 215936" src="https://github.com/user-attachments/assets/bd313518-9988-4b2b-9dd2-74832557a2d5" />

 *3. Join Client-1 to the Domain*
---
### Login to Client-1
Log in to **Client-1** using the **local administrator account**.

- Open **System Properties** and join the computer to the domain:
`mydomain.com`

<img width="423" height="465" alt="Screenshot 2026-03-02 214201" src="https://github.com/user-attachments/assets/b60aab9b-e79a-4437-b41e-9babb47918ed" />
<img width="389" height="436" alt="Screenshot 2026-03-02 214219" src="https://github.com/user-attachments/assets/62b9aade-e129-48eb-b653-cb67be42ee66" />
<img width="450" height="295" alt="Screenshot 2026-03-02 214311" src="https://github.com/user-attachments/assets/ea3975b0-2774-4567-a809-83b0865f1347" />
<img width="383" height="223" alt="Screenshot 2026-03-02 214344" src="https://github.com/user-attachments/assets/61ac94f3-9429-4f48-a7fd-ae7336322440" />

- Restart **Client-1** after joining the domain.

### Verify in Active Directory

- Log in to **DC-1** and open **Active Directory Users and Computers (ADUC)** to confirm that **Client-1** appears in the domain.

### Organize Client-1

- Create a new Organizational Unit named `_CLIENTS` and move **Client-1** into it.

<img width="623" height="413" alt="Screenshot 2026-03-02 214646" src="https://github.com/user-attachments/assets/8cd94296-409b-4b60-a766-c0c5c1e9e8a6" />
<img width="567" height="97" alt="Screenshot 2026-03-02 214753" src="https://github.com/user-attachments/assets/ae86d45a-67e5-4a2f-aecf-544745a19bbf" />

*4. Setup Remote Desktop for Non-Administrative Users on Client-1*
---

### Login to Client-1

Log in to Client-1' using the domain admin account:

* **Username:** `mydomain.com\jane_admin`
* **Password:** `your password`

### Enable Remote Desktop Access
1. Open **System Properties**.
2. Select the **Remote Desktop** tab.
3. Allow **Domain Users** access to Remote Desktop.

<img width="571" height="552" alt="Screenshot 2026-03-02 215741" src="https://github.com/user-attachments/assets/452929a3-fb38-417f-a082-d33bf6a2a499" />
<img width="668" height="607" alt="Screenshot 2026-03-02 215729" src="https://github.com/user-attachments/assets/6b64d7dc-2233-432b-a67a-e5ab7b7003f6" />
<img width="365" height="254" alt="Screenshot 2026-03-02 215750" src="https://github.com/user-attachments/assets/e669ea53-9d0b-4176-8b4c-624c18a253cb" />

### Test Remote Access

You can now log in to `Client-1` using a **non-administrative domain user**.
Note: In production environments, this is typically configured using Group Policy.

*5. Create Multiple Users with a Script*
---
### Login to DC-1

Log in to `DC-1` using the domain admin account:

* **Username:** `mydomain.com\jane_admin`

### Run the PowerShell Script

1. Open `PowerShell ISE` as **Administrator**.
2. Create a new file and paste the provided script.
3. Run the script to generate multiple user accounts. `[script](https://github.com/joshmadakor1/AD_PS/blob/master/Generate-Names-Create-Users.ps1)`

<img width="825" height="975" alt="Screenshot 2026-03-02 220839" src="https://github.com/user-attachments/assets/a388740e-230b-47e6-b80e-7d6dd3c1d653" />
<img width="397" height="129" alt="Screenshot 2026-03-02 220458" src="https://github.com/user-attachments/assets/a492263a-0a4d-4ae5-9883-b21e84c79f4a" />
<img width="397" height="129" alt="Screenshot 2026-03-02 220458" src="https://github.com/user-attachments/assets/bf0c0793-8e2d-4865-bdb3-09df814209a3" />
<img width="518" height="244" alt="Screenshot 2026-03-02 221228" src="https://github.com/user-attachments/assets/17ac5463-6f61-4211-a61d-d0585ccb2c7f" />
<img width="506" height="737" alt="Screenshot 2026-03-02 221333" src="https://github.com/user-attachments/assets/94252ef7-c599-4e10-8898-ffd5935b5d0c" />


### Verify Accounts

Open `Active Directory Users and Computers (ADUC)` and confirm the new accounts appear in the `_EMPLOYEES` OU.

<img width="616" height="504" alt="Screenshot 2026-03-02 224752" src="https://github.com/user-attachments/assets/e64fabf4-7102-474b-9730-a616d72f890a" />

### Test Login

Attempt to log in to `Client-1` using one of the newly created user accounts. Ensure the password matches the one defined in the script.

<img width="445" height="284" alt="Screenshot 2026-03-02 225658" src="https://github.com/user-attachments/assets/14d1c840-deac-4bc5-9efa-b50e021e77ab" />
<img width="535" height="320" alt="Screenshot 2026-03-02 230024" src="https://github.com/user-attachments/assets/2fd0656e-a977-40ca-b056-beab5266db92" />


<h2>Purpose</h2>
This repository documents the deployment of an Active Directory environment in Microsoft Azure using Virtual Machines. The project demonstrates core domain services, including domain controller configuration, user management, and client domain joining.

