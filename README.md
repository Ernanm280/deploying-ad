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

**1. Install Active Directory**
---
### Login to DC-1
Connect to the **DC-1 Virtual Machine** using Remote Desktop.

**Credentials**

* **Username:** `Administrator`
* **Password:** *your password*

### Install Active Directory Domain Services
1. Open **Server Manager**.
2. Click **Add Roles and Features**.
3. Select **Active Directory Domain Services (AD DS)**.
4. Complete the installation.

### Promote Server to Domain Controller
1. In **Server Manager**, click the **notification flag**.
2. Select **Promote this server to a domain controller**.
3. Choose **Add a new forest**.
4. Enter the domain name:
   
```
mydomain.com
```

5. Complete the setup and allow the server to **restart**.

### Login Using Domain Account
After the restart, log back into **DC-1**.

* **Username:** `mydomain.com\Administrator`
* **Password:** *your password*

<img width="423" height="333" alt="Screenshot 2026-03-02 210652" src="https://github.com/user-attachments/assets/8383e064-d1bd-4777-9135-028ae0059ade" />
<img width="750" height="551" alt="Screenshot 2026-03-02 210910" src="https://github.com/user-attachments/assets/ea0b0ac9-9052-47d3-9f51-2f6a5c38eaa8" />
<img width="917" height="493" alt="Screenshot 2026-03-02 211626" src="https://github.com/user-attachments/assets/20a42488-cfc1-498c-a9bb-eb59218ae48d" />

**2. Create a Domain Admin User**
---
### Open Active Directory Users and Computers
On **DC-1**, open **Active Directory Users and Computers (ADUC)**.

### Create Organizational Units
Create two Organizational Units (OUs):
* `_EMPLOYEES`
* `_ADMINS`

### Create a New User

Create a user with the following details:
* **Name:** Jane Doe
* **Username:** `jane_admin`
* **Password:** `Cyberlab123!`

Place the user in the **_ADMINS** OU.

### Add User to Domain Admins
Add `jane_admin` to the **Domain Admins** security group.

### Log in as jane_admin
Log out of **DC-1** and log back in using:

* **Username:** `mydomain.com\jane_admin`
* **Password:** `Cyberlab123!`

Use **jane_admin** as the admin account for the rest of the lab.

<img width="596" height="524" alt="Screenshot 2026-03-02 212915" src="https://github.com/user-attachments/assets/cd9e9150-f753-4118-82d8-2a0b83614fcb" />
<img width="432" height="366" alt="Screenshot 2026-03-02 212943" src="https://github.com/user-attachments/assets/0add7745-76f8-4704-86a9-67460dcc71a4" />
<img width="429" height="370" alt="Screenshot 2026-03-02 213020" src="https://github.com/user-attachments/assets/e613931c-6d8d-4fc6-bfda-d5e98dfda6c1" />
<img width="569" height="476" alt="Screenshot 2026-03-02 213255" src="https://github.com/user-attachments/assets/3eb853bf-aef8-40b1-be9d-bce5f8d61133" />
<img width="432" height="371" alt="Screenshot 2026-03-02 213358" src="https://github.com/user-attachments/assets/f7ba0b42-a954-4db2-a394-9dd5d66a6645" />
<img width="498" height="355" alt="Screenshot 2026-03-02 213609" src="https://github.com/user-attachments/assets/79e30c97-f453-480b-b5e1-605d84cee3a2" />
<img width="450" height="295" alt="Screenshot 2026-03-02 214311" src="https://github.com/user-attachments/assets/b29699a9-0154-42ef-bfb6-fc113d7b9148" />
<img width="383" height="223" alt="Screenshot 2026-03-02 214344" src="https://github.com/user-attachments/assets/7d4c0f40-4adb-4d70-8d84-c16ff30b4f33" />


 **3. Join Client-1 to the Domain**
---
### Login to Client-1
Log in to **Client-1** using the **local administrator account**.

- Open **System Properties** and join the computer to the domain:
`mydomain.com`

- Restart **Client-1** after joining the domain.

### Verify in Active Directory

- Log in to **DC-1** and open **Active Directory Users and Computers (ADUC)** to confirm that **Client-1** appears in the domain.

### Organize Client-1

- Create a new Organizational Unit named `_CLIENTS` and move **Client-1** into it.
 

<img width="921" alt="Screenshot 2025-01-23 at 3 50 00 PM" src="https://github.com/user-attachments/assets/bed85172-e5dc-4956-8762-eea8e07e5ade" />
<img width="426" alt="Screenshot 2025-01-23 at 3 50 17 PM" src="https://github.com/user-attachments/assets/47790e14-d7f2-4b27-bb08-b062aacbdca9" />
<img width="421" alt="Screenshot 2025-01-23 at 3 51 12 PM" src="https://github.com/user-attachments/assets/1c0b9cad-2fc9-4446-babe-8ec74a4ffe5a" />
<img width="277" alt="Screenshot 2025-01-23 at 3 51 25 PM" src="https://github.com/user-attachments/assets/02f62ad7-c3b6-4674-a8af-4c7d9411bc76" />
<img width="629" alt="Screenshot 2025-01-23 at 3 52 24 PM" src="https://github.com/user-attachments/assets/62af8808-9966-4ab2-a3f2-7138c65dd800" />
<img width="574" alt="Screenshot 2025-01-23 at 3 52 30 PM" src="https://github.com/user-attachments/assets/17e0e492-2047-4d5d-a6cc-459c507ca1f8" />
<img width="607" alt="Screenshot 2025-01-23 at 3 52 44 PM" src="https://github.com/user-attachments/assets/c83ed5c1-fb69-48a3-b49c-96e2a50232ba" />
<img width="728" alt="Screenshot 2025-01-23 at 3 53 02 PM" src="https://github.com/user-attachments/assets/f65d3964-2fec-47a2-a0c3-0b89f123f734" />


**4. Setup Remote Desktop for Non-Administrative Users on Client-1**
---

### Login to Client-1

Log in to **Client-1** using the domain admin account:

* **Username:** `mydomain.com\jane_admin`
* **Password:** `Cyberlab123!`

### Enable Remote Desktop Access
1. Open **System Properties**.
2. Select the **Remote Desktop** tab.
3. Allow **Domain Users** access to Remote Desktop.

### Test Remote Access

You can now log in to **Client-1** using a **non-administrative domain user**.
Note: In production environments, this is typically configured using Group Policy.


<img width="454" alt="Screenshot 2025-01-23 at 4 05 59 PM" src="https://github.com/user-attachments/assets/665b22bd-58b9-4127-a7f6-8667cb8e7b4c" />
<img width="843" alt="Screenshot 2025-01-23 at 4 06 36 PM" src="https://github.com/user-attachments/assets/1bb20155-8432-4e58-aec5-6d21b284fb1e" />
<img width="325" alt="Screenshot 2025-01-23 at 4 06 48 PM" src="https://github.com/user-attachments/assets/6cd9900d-348b-4abd-a879-a21fd617459c" />
<img width="401" alt="Screenshot 2025-01-23 at 4 07 18 PM" src="https://github.com/user-attachments/assets/e952c9c0-5d5a-4038-b759-9cee7ea85b62" />


**5. Create Additional Users and Test Login**
Here’s a **clean, simple, and concise version** that fits the style of your other sections:

---

## 5. Create Multiple Users with a Script

### Login to DC-1

Log in to **DC-1** using the domain admin account:

* **Username:** `mydomain.com\jane_admin`

### Run the PowerShell Script

1. Open **PowerShell ISE** as **Administrator**.
2. Create a new file and paste the provided script.
3. Run the script to generate multiple user accounts. [script](https://github.com/joshmadakor1/AD_PS/blob/master/Generate-Names-Create-Users.ps1)

### Verify Accounts

Open **Active Directory Users and Computers (ADUC)** and confirm the new accounts appear in the `_EMPLOYEES` OU.

### Test Login

Attempt to log in to **Client-1** using one of the newly created user accounts. Ensure the password matches the one defined in the script.


<img width="463" alt="Screenshot 2025-01-23 at 4 08 49 PM" src="https://github.com/user-attachments/assets/baaf9830-96e3-41ac-83d4-3d921678e598" />
<img width="1056" alt="Screenshot 2025-01-23 at 4 10 56 PM" src="https://github.com/user-attachments/assets/6d001fd1-8a35-4b2f-95c8-f7e307deff3d" />
<img width="1075" alt="Screenshot 2025-01-23 at 4 11 51 PM" src="https://github.com/user-attachments/assets/1672380d-8f86-4110-8ff1-6cabeeafd496" />
<img width="760" alt="Screenshot 2025-01-23 at 4 12 00 PM" src="https://github.com/user-attachments/assets/759907a3-4f8d-48f0-8c4c-038bf8bd65ac" />
<img width="785" alt="Screenshot 2025-01-23 at 4 12 32 PM" src="https://github.com/user-attachments/assets/a27ebddb-84e5-48a0-961f-b3e9cef46f2c" />
<img width="504" alt="Screenshot 2025-01-23 at 4 12 45 PM" src="https://github.com/user-attachments/assets/9cbef0ab-23fa-4e71-ba6c-e3443083a78e" />
<img width="625" alt="Screenshot 2025-01-23 at 4 18 45 PM" src="https://github.com/user-attachments/assets/5740d186-36e0-4ece-9ce5-a6803321272d" />
<img width="559" alt="Screenshot 2025-01-23 at 4 19 44 PM" src="https://github.com/user-attachments/assets/23bd76dc-d75e-41fe-8e93-846e1ae83c19" />


<h2>Purpose</h2>
This repository documents the deployment of an Active Directory environment in Microsoft Azure using Virtual Machines. The project demonstrates core domain services, including domain controller configuration, user management, and client domain joining.

