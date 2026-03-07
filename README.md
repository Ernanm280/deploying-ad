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

<img width="400" height="302" alt="image" src="https://github.com/user-attachments/assets/bff6471c-e00d-4c9b-881a-2abe50f420ec" />
<img width="400" height="315" alt="image" src="https://github.com/user-attachments/assets/f4241cbc-4f99-4b34-b527-1a5f17d1909a" />
<img width="400" height="294" alt="image" src="https://github.com/user-attachments/assets/eafdc315-a35a-417a-9473-5a16a442b7e2" />
<img width="256" height="223" alt="image" src="https://github.com/user-attachments/assets/8b735bf4-8a0d-4d52-a058-73e99ebbdc65" />


*2. Create a Domain Admin User*
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
* **Password:** `Passsword1`

Place the user in the **_ADMINS** OU.

### Add User to Domain Admins
Add `jane_admin` to the **Domain Admins** security group.

### Log in as jane_admin
Log out of **DC-1** and log back in using:

* **Username:** `mydomain.com\jane_admin`
* **Password:** `Password1`

Use **jane_admin** as the admin account for the rest of the lab.

<img width="256" height="225" alt="image" src="https://github.com/user-attachments/assets/dab997bd-f6e4-471b-a803-860dcd3677f7" />
<img width="256" height="217" alt="image" src="https://github.com/user-attachments/assets/52a74f62-e005-47dd-aabf-085c5f35f4b2" />
<img width="256" height="221" alt="image" src="https://github.com/user-attachments/assets/d162292a-7797-4d72-a3c0-5f371523eb2e" />
<img width="256" height="214" alt="image" src="https://github.com/user-attachments/assets/9f9e9cb6-395a-43ac-b38e-631ec7748ded" />
<img width="256" height="220" alt="image" src="https://github.com/user-attachments/assets/85ef7de0-8a76-477c-8a0d-17d48057460d" />
<img width="256" height="182" alt="image" src="https://github.com/user-attachments/assets/a899c185-0d11-4bab-9c64-5f291ec873b3" />


 **3. Join Client-1 to the Domain**
---
### Login to Client-1
Log in to **Client-1** using the **local administrator account**.

- Open **System Properties** and join the computer to the domain:
`mydomain.com`

- Restart **Client-1** after joining the domain.

<img width="233" height="256" alt="image" src="https://github.com/user-attachments/assets/bf3b60b6-f5f7-4754-a248-41da9bd4a37f" />
<img width="228" height="256" alt="image" src="https://github.com/user-attachments/assets/5efac0fd-df7f-4945-bcd5-92de8dd486c8" />
<img width="400" height="262" alt="image" src="https://github.com/user-attachments/assets/65ec0fa3-ba4e-467a-bea5-1fee213f8042" />
<img width="383" height="223" alt="image" src="https://github.com/user-attachments/assets/ac2e7a69-5a7d-4841-ac4c-cda18da4e9bc" />

### Verify in Active Directory

- Log in to **DC-1** and open **Active Directory Users and Computers (ADUC)** to confirm that **Client-1** appears in the domain.

### Organize Client-1

- Create a new Organizational Unit named `_CLIENTS` and move **Client-1** into it.

<img width="400" height="265" alt="image" src="https://github.com/user-attachments/assets/257c7c6d-b499-4eac-8681-9a8b87600d02" />
<img width="567" height="97" alt="image" src="https://github.com/user-attachments/assets/e317b055-2a80-4b82-93c5-8479c962bcef" />


**4. Setup Remote Desktop for Non-Administrative Users on Client-1**
---

### Login to Client-1

Log in to **Client-1** using the domain admin account:

* **Username:** `mydomain.com\jane_admin`
* **Password:** `Password1`

### Enable Remote Desktop Access
1. Open **System Properties**.
2. Select the **Remote Desktop** tab.
3. Allow **Domain Users** access to Remote Desktop.

### Test Remote Access

You can now log in to **Client-1** using a **non-administrative domain user**.
Note: In production environments, this is typically configured using Group Policy.

<img width="256" height="174" alt="image" src="https://github.com/user-attachments/assets/fe242b76-fcda-4ab6-bac3-ca70028b5ea9" />
<img width="298" height="112" alt="image" src="https://github.com/user-attachments/assets/1a09ee38-ac2c-410b-941d-9eae47e005cc" />
<img width="256" height="247" alt="image" src="https://github.com/user-attachments/assets/1d151898-0a1d-4e70-a81c-04880e6a07cd" />
<img width="256" height="232" alt="image" src="https://github.com/user-attachments/assets/986e03cd-f6f1-45d8-861c-469c952366da" />
<img width="365" height="254" alt="image" src="https://github.com/user-attachments/assets/b7f55be0-d64b-46f9-a827-463bb0cc9e6b" />


## 5. Create Multiple Users with a Script

### Login to DC-1

Log in to **DC-1** using the domain admin account:

* **Username:** `mydomain.com\jane_admin`

### Run the PowerShell Script

1. Open **PowerShell ISE** as **Administrator**.
2. Create a new file and paste the provided script.
3. Run the script to generate multiple user accounts. [script](https://github.com/joshmadakor1/AD_PS/blob/master/Generate-Names-Create-Users.ps1)

<img width="216" height="256" alt="image" src="https://github.com/user-attachments/assets/79297155-5bca-4819-82ce-99d3a430080f" />
<img width="397" height="129" alt="image" src="https://github.com/user-attachments/assets/5c405b71-a0e1-4e7b-a89b-0f40d29c66c9" /><img width="315" height="180" alt="image" src="https://github.com/user-attachments/assets/71f02358-d218-436a-804c-0d12f2d15d39" />
<img width="256" height="237" alt="image" src="https://github.com/user-attachments/assets/a5e57878-0164-4001-ac51-e9ec03870c8b" />
<img width="393" height="185" alt="image" src="https://github.com/user-attachments/assets/a936fa3b-8b5a-4c87-a522-0ca403104cc2" />
<img width="256" height="190" alt="image" src="https://github.com/user-attachments/assets/05becdb2-3d30-4424-ad0d-9ac772936016" />

### Verify Accounts

Open **Active Directory Users and Computers (ADUC)** and confirm the new accounts appear in the `_EMPLOYEES` OU.

<img width="400" height="327" alt="image" src="https://github.com/user-attachments/assets/3c3d49d1-4fcd-4f99-b5d0-8e21870d5c38" />

### Test Login

Attempt to log in to **Client-1** using one of the newly created user accounts. Ensure the password matches the one defined in the script.


<img width="256" height="182" alt="image" src="https://github.com/user-attachments/assets/f2a28887-2852-4aa6-97a3-96528c55d4fc" />


<h2>Purpose</h2>
This repository documents the deployment of an Active Directory environment in Microsoft Azure using Virtual Machines. The project demonstrates core domain services, including domain controller configuration, user management, and client domain joining.

