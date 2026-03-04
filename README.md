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
- Login to `DC-1`
  - Use the credentials:
    - Username: 
    - Password: 
- Install Active Directory Domain Services
  - Open Server Manager and install the Active Directory Domain Services role.
- Promote as a Domain Controller
  - Set up a new forest with the domain name `mydomain.com` (or any preferred name).
  - Restart the server after promotion.
- Login to `DC-1` as Domain User
  - Use the credentials:
    - Username: `mydomain.com\`


<img width="830" alt="Screenshot 2025-01-23 at 3 39 35 PM" src="https://github.com/user-attachments/assets/4e576c4c-b6dd-4aa6-bf85-6070571682bf" />
<img width="671" alt="Screenshot 2025-01-23 at 3 39 41 PM" src="https://github.com/user-attachments/assets/3d8b8ec4-0942-4669-91e5-20bad33d35a5" />
<img width="1223" alt="Screenshot 2025-01-23 at 3 40 40 PM" src="https://github.com/user-attachments/assets/f4febafe-d041-48c5-a1e3-6f2f18458b75" />
<img width="571" alt="Screenshot 2025-01-23 at 3 40 54 PM" src="https://github.com/user-attachments/assets/55020542-5ab2-4d7e-8b18-2307480e6dc0" />
<img width="421" alt="Screenshot 2025-01-23 at 3 42 14 PM" src="https://github.com/user-attachments/assets/1378c546-4afc-4e90-891e-c95eea98e73e" />


**2. Create a Domain Admin User**
- Open Active Directory Users and Computers (ADUC)
- Create Organizational Units (OUs)
  - Create an OU named `_EMPLOYEES`.
  - Create another OU named `_ADMINS`.
- Create a New Employee User
  - Add a user named "Jane Doe" with the following details:
    - Username: `jane_admin`
    - Password: `Cyberlab123!`
- Add User to Security Group
  - Add `jane_admin` to the Domain Admins Security Group.
- Log in as `jane_admin`
  - Log out from `DC-1` and log back in using:
    - Username: `mydomain.com\jane_admin`
    - Password: `Cyberlab123!`
  - Use `jane_admin` as the admin account from this point forward.


<img width="692" alt="Screenshot 2025-01-23 at 3 45 08 PM" src="https://github.com/user-attachments/assets/52a900c0-8050-413f-a57b-39d41995e8e1" />
<img width="684" alt="Screenshot 2025-01-23 at 3 45 28 PM" src="https://github.com/user-attachments/assets/d756cefa-8fee-43ff-83aa-949763c18fdb" />
<img width="664" alt="Screenshot 2025-01-23 at 3 45 52 PM" src="https://github.com/user-attachments/assets/b6c24ef3-1556-4afd-9721-bdca545410e5" />
<img width="1335" alt="Screenshot 2025-01-23 at 3 46 19 PM" src="https://github.com/user-attachments/assets/9fc14a7e-9c00-42b5-9fbf-d268e6fe78f3" />
<img width="651" alt="Screenshot 2025-01-23 at 3 46 30 PM" src="https://github.com/user-attachments/assets/ef0c6e97-061e-4331-8cd3-462490184e8d" />
<img width="406" alt="Screenshot 2025-01-23 at 3 47 10 PM" src="https://github.com/user-attachments/assets/801c5acf-9a74-4240-a73c-de9353dfc8e0" />
<img width="533" alt="Screenshot 2025-01-23 at 3 47 30 PM" src="https://github.com/user-attachments/assets/fe2e062a-080e-4259-87f6-289556859abc" />


 
**3. Join `Client-1` to the Domain**
- Login to `Client-1` as Local Admin
- Join `Client-1` to the Domain
  - Change the system properties to join the domain `mydomain.com.`
  - Restart `Client-1` after joining.
- Verify in ADUC
  - Log in to `DC-1` and confirm that `Client-1` appears in the Active Directory Users and Computers tool.
- Organize `Client-1` in ADUC
  - Create an OU named `_CLIENTS`.
  - Drag `Client-1` into the `_CLIENTS OU`.


<img width="921" alt="Screenshot 2025-01-23 at 3 50 00 PM" src="https://github.com/user-attachments/assets/bed85172-e5dc-4956-8762-eea8e07e5ade" />
<img width="426" alt="Screenshot 2025-01-23 at 3 50 17 PM" src="https://github.com/user-attachments/assets/47790e14-d7f2-4b27-bb08-b062aacbdca9" />
<img width="421" alt="Screenshot 2025-01-23 at 3 51 12 PM" src="https://github.com/user-attachments/assets/1c0b9cad-2fc9-4446-babe-8ec74a4ffe5a" />
<img width="277" alt="Screenshot 2025-01-23 at 3 51 25 PM" src="https://github.com/user-attachments/assets/02f62ad7-c3b6-4674-a8af-4c7d9411bc76" />
<img width="629" alt="Screenshot 2025-01-23 at 3 52 24 PM" src="https://github.com/user-attachments/assets/62af8808-9966-4ab2-a3f2-7138c65dd800" />
<img width="574" alt="Screenshot 2025-01-23 at 3 52 30 PM" src="https://github.com/user-attachments/assets/17e0e492-2047-4d5d-a6cc-459c507ca1f8" />
<img width="607" alt="Screenshot 2025-01-23 at 3 52 44 PM" src="https://github.com/user-attachments/assets/c83ed5c1-fb69-48a3-b49c-96e2a50232ba" />
<img width="728" alt="Screenshot 2025-01-23 at 3 53 02 PM" src="https://github.com/user-attachments/assets/f65d3964-2fec-47a2-a0c3-0b89f123f734" />


**4. Setup Remote Desktop for Non-Administrative Users on Client-1**

- Login to `Client-1` as `mydomain.com\jane_admin`
  - Use the credentials for `jane_admin`.
- Allow Domain Users Access to Remote Desktop
  - Open system properties.
  - Click on "Remote Desktop."
  - Allow "domain users" access to Remote Desktop.
- Test Remote Desktop Access
  - You can now log into `Client-1` as a normal, non-administrative user.
   -Note: Typically, this configuration is managed using Group Policy for multiple systems.


<img width="454" alt="Screenshot 2025-01-23 at 4 05 59 PM" src="https://github.com/user-attachments/assets/665b22bd-58b9-4127-a7f6-8667cb8e7b4c" />
<img width="843" alt="Screenshot 2025-01-23 at 4 06 36 PM" src="https://github.com/user-attachments/assets/1bb20155-8432-4e58-aec5-6d21b284fb1e" />
<img width="325" alt="Screenshot 2025-01-23 at 4 06 48 PM" src="https://github.com/user-attachments/assets/6cd9900d-348b-4abd-a879-a21fd617459c" />
<img width="401" alt="Screenshot 2025-01-23 at 4 07 18 PM" src="https://github.com/user-attachments/assets/e952c9c0-5d5a-4038-b759-9cee7ea85b62" />


**5. Create Additional Users and Test Login**

- Login to `DC-1` as `jane_admin`
  - Use the credentials for `jane_admin`.
- Open PowerShell ISE as Administrator
  - Launch PowerShell ISE with administrative privileges.
- Create Users with a Script
  - Create a new file and paste the provided [script](https://github.com/joshmadakor1/AD_PS/blob/master/Generate-Names-Create-Users.ps1) into it.
  - Run the script to create multiple user accounts.
- Verify Accounts in ADUC
  - Open Active Directory Users and Computers (ADUC).
  - Observe the newly created accounts in the `_EMPLOYEES OU`.
- Test Login
  - Attempt to log into `Client-1` using one of the newly created accounts.
  - Ensure the account password matches what is specified in the script.


<img width="463" alt="Screenshot 2025-01-23 at 4 08 49 PM" src="https://github.com/user-attachments/assets/baaf9830-96e3-41ac-83d4-3d921678e598" />
<img width="1056" alt="Screenshot 2025-01-23 at 4 10 56 PM" src="https://github.com/user-attachments/assets/6d001fd1-8a35-4b2f-95c8-f7e307deff3d" />
<img width="1075" alt="Screenshot 2025-01-23 at 4 11 51 PM" src="https://github.com/user-attachments/assets/1672380d-8f86-4110-8ff1-6cabeeafd496" />
<img width="760" alt="Screenshot 2025-01-23 at 4 12 00 PM" src="https://github.com/user-attachments/assets/759907a3-4f8d-48f0-8c4c-038bf8bd65ac" />
<img width="785" alt="Screenshot 2025-01-23 at 4 12 32 PM" src="https://github.com/user-attachments/assets/a27ebddb-84e5-48a0-961f-b3e9cef46f2c" />
<img width="504" alt="Screenshot 2025-01-23 at 4 12 45 PM" src="https://github.com/user-attachments/assets/9cbef0ab-23fa-4e71-ba6c-e3443083a78e" />
<img width="625" alt="Screenshot 2025-01-23 at 4 18 45 PM" src="https://github.com/user-attachments/assets/5740d186-36e0-4ece-9ce5-a6803321272d" />
<img width="559" alt="Screenshot 2025-01-23 at 4 19 44 PM" src="https://github.com/user-attachments/assets/23bd76dc-d75e-41fe-8e93-846e1ae83c19" />


<h2>Purpose</h2>
The purpose of this repository is to provide a comprehensive guide for deploying Active Directory through virtual machines on Azure. This implementation is intended to replicate on-premises infrastructure within a cloud environment, enabling scalable and manageable domain services for various organizational needs.

