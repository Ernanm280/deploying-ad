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

**1. Create a Domain Admin User**
---

I begin by opening an `RDP` session to the **DC-1** VM using the original admin user created in Azure, but with domain credentials `mydomain.com\<yourcreatedcredentials>` and password. Once logged into the VM, I ran **Active Directory Users and Computers (ADUC)** as an administrator.

<img width="871" height="561" alt="Screenshot 2026-04-11 175157" src="https://github.com/user-attachments/assets/1ca449f4-7cf6-42d1-9308-51dcd98b4555" />

<br>
<br>

Within **Active Directory Users and Computers**, I right-clicked the domain (mydomain.com), selected New → Organizational Unit, and created two Organizational Units (OUs) named _EMPLOYEES and _ADMINS. These OUs will be used to logically separate standard user accounts from administrative accounts, allowing for better organization and easier management of permissions and Group Policy.

<br>
<br>

<img width="742" height="522" alt="Screenshot 2026-04-11 175310" src="https://github.com/user-attachments/assets/74bb778f-e0d1-4d6f-b790-92036e783282" />

<br>
<br>

Within **Active Directory Users and Computers**, I navigated to the **_ADMINS** Organizational Unit, right-clicked, and selected New → User to create a new administrative account. I entered the user’s details, including the name **Jane Doe**, and assigned the username jane_admin in the **mydomain.com** domain. After completing the required fields, on the Password screen, I unchecked “User must change password at next logon”, enabled “Password never expires”, and then set a password for the account. This account will be used as an administrative account, separate from standard user accounts, to follow best practices for privilege management.

<img width="566" height="361" alt="Screenshot 2026-04-11 175719" src="https://github.com/user-attachments/assets/758d793f-132b-4e22-bf9f-27b91c9af5ef" />
<img width="431" height="372" alt="Screenshot 2026-04-11 180028" src="https://github.com/user-attachments/assets/b6d1ec71-b1c3-4874-a645-7aa8f54266ac" />
<img width="433" height="372" alt="Screenshot 2026-04-11 180107" src="https://github.com/user-attachments/assets/7d233b61-2626-407a-87e4-58432ba8f64d" />

<br>
<br>

We verify that Jane Admin is in the designated group, the _ADMINS (OU). 

<img width="605" height="181" alt="Screenshot 2026-04-11 180140" src="https://github.com/user-attachments/assets/77ccfc53-c6c1-48d7-9e5e-355ff1e339e2" />

<br>
<br>

Right-clicking **Jane Doe** (administrative account), in the user’s **Properties**, under the **Member Of** tab, I selected **Add**, entered "Domain Admins", and clicked **Check Names** to validate the group. After confirming, I clicked **OK** to add the user to the Domain Admins group, granting administrative privileges.
Adding the user to the Domain Admins group provides full administrative control over the domain, following the practice of using dedicated admin accounts instead of default ones.

<img width="526" height="360" alt="Screenshot 2026-04-11 180608" src="https://github.com/user-attachments/assets/2a31d849-d070-4831-baf1-3eb5786c822f" />
<img width="862" height="492" alt="Screenshot 2026-04-11 180425" src="https://github.com/user-attachments/assets/1cc42884-f965-437b-be6e-7e74b73df1e6" />

<br>
<br>

Logged out of `DC-1` and logged back in using the domain credentials `mydomain.com\jane_admin` as the username and password. For the remaining steps, we will keep `RDP` open to use **jane_admin** as the admin account for the rest of the lab.

<img width="932" height="664" alt="Screenshot 2026-04-11 181050" src="https://github.com/user-attachments/assets/238283f0-873f-4143-8d15-b2fb112dccab" />

**2. Join Client-1 to the Domain**
---

Navigate to the Azure Virtual machine list and select **Client-1** VM, initiate `RDP` with the IP address (52.186.171.6) using domain credentials `mydomain.com\<yourcreatedcredentials>` and password. 

<img width="977" height="430" alt="Screenshot 2026-04-11 181442" src="https://github.com/user-attachments/assets/a4cef92b-b067-4e0f-9735-850ee3df86d0" />

<br>
<br>

After logging in, I right-clicked the Start menu and selected **System** to access the computer’s system settings and configuration details. 
On the right-hand side, I selected **Rename this PC (advanced)** > **Change**, which opened the **System Properties** window. Under the Computer Name tab, I selected Change to modify the computer’s domain membership. I then chose the Domain option, entered mydomain.com, and clicked **OK** to join **Client-1** to the domain.

<img width="849" height="411" alt="Screenshot 2026-04-11 181635" src="https://github.com/user-attachments/assets/378ec3bd-030e-4533-9661-42ccff34a347" />
<img width="1187" height="723" alt="Screenshot 2026-04-11 181806" src="https://github.com/user-attachments/assets/07c87cf1-3305-4eb4-90b2-77657e21fe35" />

<br>
<br>

After entering valid domain credentials, the computer was successfully joined to the domain and required a restart to apply the changes. Joining the computer to the domain allows centralized management of users, security policies, and resources through Active Directory, making administration more efficient and scalable.

<img width="452" height="366" alt="Screenshot 2026-04-11 182131" src="https://github.com/user-attachments/assets/223f557d-f709-4398-b4b3-219322e77ac3" />
<img width="297" height="151" alt="Screenshot 2026-04-11 182234" src="https://github.com/user-attachments/assets/1dccc76b-9674-48d3-b6cd-76c0d102af37" />
<img width="348" height="181" alt="Screenshot 2026-04-11 182247" src="https://github.com/user-attachments/assets/01064df1-4b64-495f-9121-78be19810ce8" />

### Verify in Active Directory

I went back to the Domain Controller VM `DC-1`, opened **Active Directory Users and Computers**, and verified that (Client-1) appeared in the Computers folder under the domain ** mydomain.com **, confirming it was successfully added to the domain.

<img width="473" height="214" alt="Screenshot 2026-04-11 182637" src="https://github.com/user-attachments/assets/a207a2ea-5ab2-4620-ab2d-0e0965ac7a74" />

<br>
<br>

By separating administrators, employees, and client systems into distinct containers for improved organization and management, I create a new Organizational Unit named `_CLIENTS` and move `Client-1` into it.

<img width="582" height="457" alt="Screenshot 2026-04-11 182738" src="https://github.com/user-attachments/assets/882960f6-8834-4522-8b97-976c7f8a774f" />
<img width="499" height="191" alt="Screenshot 2026-04-11 182847" src="https://github.com/user-attachments/assets/a18c30de-97af-4ac1-81dd-2b5e8a0ee614" />

**3. Set up Remote Desktop for Non-Administrative Users**
---
Log in to the **Client-1** VM domain admin username `mydomain.com\jane_admin`, and password. Once logged in, I right-clicked the Start menu and selected **System** to open Remote Desktop Settings, then enabled Remote Desktop by selecting “Select users that can remotely access this PC”. In the Object names field, I typed "Domain User" and selected **Check Names** to validate. After confirming, I clicked **OK** to grant all domain users remote access.

This configuration allows authorized domain users to remotely connect to the client machine using Remote Desktop Protocol (RDP), enabling centralized and flexible access to the system.

<img width="1190" height="708" alt="Screenshot 2026-04-11 183149" src="https://github.com/user-attachments/assets/3de897ab-51ae-45e2-bdbd-41c5d72c6e3c" />
<img width="369" height="153" alt="Screenshot 2026-04-11 183207" src="https://github.com/user-attachments/assets/41315fdf-405c-4a04-b271-fa9cd87bab14" />


### Test Remote Access

You can now log in to `Client-1` using a **non-administrative domain user**.
Note: In production environments, this is typically configured using Group Policy.

---
 
**4. Create Multiple Users with a Script**

### Login to DC-1

Log in to `DC-1` using the domain admin account:

* **Username:** `mydomain.com\jane_admin`

### Run the PowerShell Script

1. Open `PowerShell ISE` as **Administrator**.
2. Create a new file and paste the provided script.
3. Run the script to generate multiple user accounts. `[script](https://github.com/joshmadakor1/AD_PS/blob/master/Generate-Names-Create-Users.ps1)`

<img width="825" height="975" alt="Screenshot 2026-03-02 220839" src="https://github.com/user-attachments/assets/a388740e-230b-47e6-b80e-7d6dd3c1d653" />
<img width="397" height="129" alt="Screenshot 2026-03-02 220458" src="https://github.com/user-attachments/assets/a492263a-0a4d-4ae5-9883-b21e84c79f4a" />
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

