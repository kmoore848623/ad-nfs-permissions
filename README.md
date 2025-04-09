![NFS_Permissions_Azure_Small](https://github.com/user-attachments/assets/c9e94a9a-f15e-46c1-b2bc-9bd9f322a049)


# Network File Shares and Permissions Using Azure Virtual Machines

This project demonstrates the setup of file shares with customized permission levels (Read, Write, No Access) using Active Directory groups on Azure Virtual Machines. Users are granted or denied access based on group membership.

---

## 🧰 Technologies Used

- Microsoft Azure (Virtual Machines)
- Remote Desktop
- Active Directory Domain Services
- NTFS Permissions & Security Groups

---

## 🖥️ Operating Systems

- Windows Server 2022 (Domain Controller)
- Windows 10 (Client Machine)

---


## 🛠️ Deployment Steps

### Step 1: Reset User Password

Reset the password of a domain user on the **Domain Controller (DC)** to log in from the **Client VM**.

![Reset Password](images/reset-user-password.png)

---

### Step 2: Create Folder Structure

Create the following folders on the C:\ drive of the DC:
- `read-access`
- `write-access`
- `no-access`
- `accounting`

![Create Folders](images/create-access-folders.png)

---

### Step 3: Assign Permissions

- **Domain Users**:
  - Read-only to `read-access`
  - Read/Write to `write-access`
- **Domain Admins**:
  - Full control of `no-access`

![Read Permissions](images/read-permissions.png)
![Write Permissions](images/write-permissions.png)
![Admin Permissions](images/admin-permissions.png)

---

### Step 4: Test Folder Access from Client VM

Log in to the Client VM using a **Domain User** account and try accessing each folder.
- Access to `read-access` and `write-access` should succeed.
- Access to `no-access` should be denied.

![Client Read](images/client-access-read.png)
![Client Write](images/client-access-write.png)
![Client Denied](images/client-denied-access.png)

---

### Step 5: Create a Security Group for Accountants

- On the DC, create a new group called **ACCOUNTANTS**.
- Assign read/write permissions to the `accounting` folder for this group.

![Create ACCOUNTANTS](images/create-accountants-group.png)
![Assign Access](images/assign-accountants-access.png)

---

### Step 6: User Access to Accounting Folder

- Attempt to access the `accounting` folder using a user **not** in the group (access should fail).
- Add the user to the **ACCOUNTANTS** group in AD.
- Re-attempt folder access (access should succeed).

![No Access](images/no-access-user.png)
![Add to Group](images/add-user-to-accountants.png)
![Access Granted](images/user-gains-access.png)

---

## 💡 Notes

- Always verify group memberships via Active Directory.
- File permissions may take a few seconds to propagate.
- Use `gpupdate /force` on client machines if needed.
