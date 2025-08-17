<p align="center">
  <img src="https://github.com/user-attachments/assets/62d83ac7-7b6c-4128-b857-6ab6d17536a3" alt="Description" width="600">
</p>

---
## Platforms and Languages Leveraged
- Azure 2025 Microsoft Windows Server Datacenter 
  
---

## Project

Active Directory Onboarding Project – Demonstrates OU, user, group, GPO management, delegation, auditing, and role-based access control in a small-to-mid-sized company scenario.

---

## Scenario

Your small-to-mid-sized company is onboarding new employees across several departments. HR has requested accounts for 8 new hires: some are standard staff, others are team leads with administrative rights. Additionally, there is one IT contractor requiring temporary access. You are tasked with structuring the Active Directory environment, applying security policies, and demonstrating role-based access control.

---

## Email from HR

Subject: New Employee Onboarding Request
From: HR Department
To: IT Administrator

Hi Kyle,

We have 8 new employees joining across multiple departments. Please create their AD accounts and assign permissions based on their roles:

HR:
Sarah Thompson – HR Manager,
John Davis – HR Staff,
Emily Chen – HR Staff

IT:
Michael Lee – IT Staff,
Priya Patel – IT Staff,
James Miller – IT Contractor (3 months only)

Sales:
Rachel Green – Sales Staff
David Wilson – Sales Team Lead

Apply standard security policies for passwords and desktop restrictions. Let us know once accounts are ready.

Thanks,
HR Team

---

## Security hardening and policy management

Password Policy and IT Desktop Restrictions within Group Policy Management

<img width="1602" height="1052" alt="image" src="https://github.com/user-attachments/assets/6b054e07-a826-4760-b558-be6b163fd9be" />

---

Password Policy:

<img width="1576" height="1070" alt="image" src="https://github.com/user-attachments/assets/1f77d2d6-c2c7-451f-ac54-506f78ae78d5" />

---

Lockot Policy:

<img width="1740" height="1076" alt="image" src="https://github.com/user-attachments/assets/94338130-7273-4b3e-9d70-c1f96431a234" />

---

Preventing Removable Devices Access:

<img width="1212" height="568" alt="Screen Shot 2025-08-16 at 1 46 42 PM" src="https://github.com/user-attachments/assets/32ba700e-ba5f-4b50-99b2-926f2cc84d86" />

---

Stricter IT Desktop Restrictions: 

<img width="2338" height="1142" alt="image" src="https://github.com/user-attachments/assets/6c7b9912-59e9-456b-84d9-249da8bbfe1e" />


<img width="2428" height="1140" alt="image" src="https://github.com/user-attachments/assets/2a5df704-41d4-42b8-9f87-a8eca7775179" />

---

## Account creation

### Creating Sarah Thompson's AD profile manually in AD:

<img width="750" height="501" alt="image" src="https://github.com/user-attachments/assets/e688a6cc-b12e-48c6-92e6-4d742c6794da" />

Prompts following user name:

<img width="862" height="759" alt="image" src="https://github.com/user-attachments/assets/6a840ea8-0973-46f5-9530-405aa09cff38" />

<img width="871" height="752" alt="image" src="https://github.com/user-attachments/assets/cd8a1827-ef71-4f10-9b59-2a8af7057334" />

___

Setting Sarah as the Manager in IT: 

<img width="811" height="621" alt="image" src="https://github.com/user-attachments/assets/714c4032-daaf-4ef6-8b51-838b67d53857" />

___

To save time I created a powershell script to port these new employees over to AD via powershell

Powershell script:

New-ADUser -Name "Sarah Thompson" -GivenName Sarah -Surname Thompson -SamAccountName sthompson -UserPrincipalName sthompson@corp.local -Path "OU=HR,DC=corp,DC=local" -AccountPassword (Read-Host -AsSecureString "Pass") -Enabled $true
Add-ADGroupMember -Identity "HR-Admins" -Members "sthompson"

New-ADUser -Name "John Davis" -GivenName John -Surname Davis -SamAccountName jdavis -UserPrincipalName jdavis@corp.local -Path "OU=HR,DC=corp,DC=local" -AccountPassword (Read-Host -AsSecureString "Pass") -Enabled $true
Add-ADGroupMember -Identity "HR-Employees" -Members "jdavis"

New-ADUser -Name "Emily Chen" -GivenName Emily -Surname Chen -SamAccountName echen -UserPrincipalName echen@corp.local -Path "OU=HR,DC=corp,DC=local" -AccountPassword (Read-Host -AsSecureString "Pass") -Enabled $true
Add-ADGroupMember -Identity "HR-Employees" -Members "echen"

### After running the powershell script I verified each new HR employees ported over successfully: 

<img width="1487" height="1050" alt="image" src="https://github.com/user-attachments/assets/3233efff-9f55-46e3-b1ec-2f5ba9449888" />

___

### Porting new IT employees over

This will be the same as the HR employees with an exception of an IT contractor that is a temp. Their profile will be disabled in 3 months. 

### Creating James Miller's AD profile manually to showcase how a temp employee is setup:

<img width="1506" height="1006" alt="image" src="https://github.com/user-attachments/assets/b1c0d18c-f68d-4421-a4d2-b1f00a1ec5ea" />
___
<img width="434" height="377" alt="image" src="https://github.com/user-attachments/assets/700918ca-8eb7-4fce-829d-7ae547248d6f" />
___
<img width="434" height="375" alt="image" src="https://github.com/user-attachments/assets/309f48a0-070f-4f9a-9f05-3ae4a261ed3a" />
___

When in properties for Mr. Miller I verified under member of that they are associated with the IT' Contractors group

<img width="410" height="309" alt="image" src="https://github.com/user-attachments/assets/31d2584e-6ffc-4b34-9dd4-111c3fe1dce7" />

___

Setting James Miller's AD profile to expire in 3 months

<img width="1032" height="465" alt="image" src="https://github.com/user-attachments/assets/e3105282-1ec1-4872-9e20-7b9f42099315" />
___

Powershell script:

New-ADUser -Name "Michael Lee" -GivenName Michael -Surname Lee -SamAccountName mlee -UserPrincipalName mlee@corp.local -Path "OU=IT,DC=corp,DC=local" -AccountPassword (Read-Host -AsSecureString "Pass") -Enabled $true
Add-ADGroupMember -Identity "IT-Employees" -Members "mlee"

New-ADUser -Name "Priya Patel" -GivenName Priya -Surname Patel -SamAccountName ppatel -UserPrincipalName ppatel@corp.local -Path "OU=IT,DC=corp,DC=local" -AccountPassword (Read-Host -AsSecureString "Pass") -Enabled $true
Add-ADGroupMember -Identity "IT-Employees" -Members "ppatel"

New-ADUser -Name "James Miller" -GivenName James -Surname Miller -SamAccountName jmiller -UserPrincipalName jmiller@corp.local -Path "OU=IT,DC=corp,DC=local" -AccountPassword (Read-Host -AsSecureString "Pass") -Enabled $true
Set-ADUser -Identity jmiller -AccountExpirationDate (Get-Date).AddMonths(3)
Add-ADGroupMember -Identity "IT-Contractors" -Members "jmiller"

___

### After running the powershell script I verified each new IT employees ported over successfully: 

<img width="750" height="502" alt="image" src="https://github.com/user-attachments/assets/29122154-9eda-471d-ae7c-943a6fea8e2a" />
___
### Porting new Sales employees over
___
Powershell script:

New-ADUser -Name "Rachel Green" -GivenName Rachel -Surname Green -SamAccountName rgreen -UserPrincipalName rgreen@corp.local -Path "OU=Sales,DC=corp,DC=local" -AccountPassword (Read-Host -AsSecureString "Pass") -Enabled $true
Add-ADGroupMember -Identity "Sales-Employees" -Members "rgreen"

New-ADUser -Name "David Wilson" -GivenName David -Surname Wilson -SamAccountName dwilson -UserPrincipalName dwilson@corp.local -Path "OU=Sales,DC=corp,DC=local" -AccountPassword (Read-Host -AsSecureString "Pass") -Enabled $true
Add-ADGroupMember -Identity "Sales-Admins" -Members "dwilson"

___

### After running the powershell script I verified each new Sales employees ported over successfully: 

<img width="751" height="529" alt="image" src="https://github.com/user-attachments/assets/3dccb746-0b97-4fd7-842e-75d4b60e0035" />

___

## Created Audit Policy and linked at the domain level corp.local therefore applying this GPO to all OU's:

<img width="801" height="528" alt="image" src="https://github.com/user-attachments/assets/da1abd2c-b898-49e4-b2b8-97b3aee2032d" />
___

<img width="802" height="505" alt="image" src="https://github.com/user-attachments/assets/0955d55c-9da4-45a0-bd8d-ca31b452bb28" />

___

Once all of this was done. I recieved a follow up email from HR requesting HR manager Sarah Thompson be able to reset passwords and create/delete user accounts within the HR OU.
___
### Follow up Email from HR

Subject: Special Permissions for HR Manager
From: HR Department
To: IT Administrator

Hi Kyle,

We’d like HR Manager Sarah Thompson to be able to handle basic account management tasks for her team without needing full admin rights. Please delegate permissions so she can reset passwords and create/delete user accounts within the HR OU.

Thank you,
HR Team
___

### Delegate Control to Sarah (via Wizard)

<img width="745" height="498" alt="image" src="https://github.com/user-attachments/assets/7c5dc7a8-0c18-49f2-8214-e0a3943357fc" />
___
Step 1:

<img width="498" height="392" alt="image" src="https://github.com/user-attachments/assets/00fa4408-dfaf-4be0-8aaf-4a84c208a99b" />
___
Step 2:

<img width="497" height="346" alt="image" src="https://github.com/user-attachments/assets/f4432d23-2dc7-4c16-b714-160c45f826ba" />
___
Step 3: 

<img width="499" height="392" alt="image" src="https://github.com/user-attachments/assets/d37b8e05-7c2e-4227-b858-0d6eb4450415" />
___

Finializing:

<img width="497" height="390" alt="image" src="https://github.com/user-attachments/assets/246f4db5-8954-4172-943b-8f07ba7d1a02" />

___

## GROUP POLICY MANAGEMENT EDITOR

For the final test, I launched the `Group Policy Management` Console by pressing `Win + R`, typing `gpmc.msc`, and pressing Enter. This opened the `Group Policy Management Editor`, allowing me to explore how `Group Policy Objects` (GPOs) are created, linked to `Organizational Units` (OUs), and used to manage user and computer configurations across the domain.

Within the `Group Policy Management Editor`, I navigated to `Computer Configuration` > `Policies` > `Windows Settings` > `Security Settings` > `Account Policies` > `Password Policy` to enforce stricter password requirements and establish an account lockout policy across the domain.

<img width="804" height="319" alt="Lab 122" src="https://github.com/user-attachments/assets/68ff421b-cdaf-461d-9426-92568e8ef5eb" /></br>

<img width="802" height="318" alt="Lab 123" src="https://github.com/user-attachments/assets/0a040ab2-f4cc-40ff-9981-a5c5d72e53ef" /></br>

To enable auditing for user activity, I configured `audit policies` to track logon events, logoffs, and account lockouts. These settings allow security teams to monitor authentication activity and detect potential unauthorized access attempts, account misuse, or lockout patterns across the domain.

<img width="803" height="592" alt="Lab 127" src="https://github.com/user-attachments/assets/8ca1e105-1c55-451e-b869-a5d740ab74a8" /></br>

These audits can be analyzed in `Event Viewer` (`Win + R` > `eventvwr.msc`) under `Windows Logs` > `Security`.

<img width="1156" height="595" alt="Lab 132" src="https://github.com/user-attachments/assets/0e675f68-a347-40b9-a058-6251d1ee5677" /></br>

| Task Category   | Event ID | Description                                                |
|:----------------|:---------|:-----------------------------------------------------------|
| Logon           | 4624     | Successful user logon                                      |
| Logoff          | 4634     | User logoff                                                |
| Logon Failure   | 4625     | Failed user logon attempt                                  |
| Account Lockout | 4740     | A user account was locked out due to failed login attempts |
| Special Logon   | 4672     | Logon with special privileges (e.g., admin rights)         |

___




