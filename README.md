
# Password Protect and Remove Password from GRUB Menu (RHEL/CentOS/Fedora)

## 📌 Objective
Secure the GRUB boot menu with a password or remove an existing password on RHEL, CentOS, and Fedora Linux systems.

---

## 🔐 Password Protect GRUB Menu

### 1. Create a GRUB Password
```bash
grub2-mkpasswd-pbkdf2
```

### Example Output:
```
Enter password: ********
Reenter password: ********
PBKDF2 hash of your password is grub.pbkdf2.sha512.10000.XXXXXXXXXXXXXXXXXXXXXXXXXXXX
```

Copy the full hash.

---

### 2. Edit GRUB Configuration
Edit the GRUB config file:
```bash
sudo nano /etc/grub.d/40_custom
```

Add the following lines:
```bash
set superusers="admin"
password_pbkdf2 admin grub.pbkdf2.sha512.10000.XXXXXXXXXXXXXXXXXXXXXXXXXXXX
```

Replace `"admin"` with your desired username and paste the hash from earlier.

---

### 3. Update GRUB
Run the appropriate command based on your system:
- For BIOS systems:
```bash
sudo grub2-mkconfig -o /boot/grub2/grub.cfg
```

- For UEFI systems:
```bash
sudo grub2-mkconfig -o /boot/efi/EFI/redhat/grub.cfg
```

---

### 4. Test It
Reboot your system. When editing boot entries or accessing recovery mode, GRUB will now ask for a username and password.

---

## 🔓 Remove Password from GRUB Menu

### 1. Edit GRUB Configuration
Open the GRUB custom config file:
```bash
sudo nano /etc/grub.d/40_custom
```

Remove or comment out these lines:
```bash
set superusers="admin"
password_pbkdf2 admin grub.pbkdf2.sha512.10000.XXXXXXXXXXXXXXXXXXXXXXXXXXXX
```

---

### 2. Regenerate GRUB Configuration
Run:
- For BIOS:
```bash
sudo grub2-mkconfig -o /boot/grub2/grub.cfg
```

- For UEFI:
```bash
sudo grub2-mkconfig -o /boot/efi/EFI/redhat/grub.cfg
```

---

### ✅ Done!
The GRUB menu will no longer prompt for a password.

---

## 🛑 Important Notes
- Backup configuration files before editing.
- Use a strong password for GRUB protection.
- Test thoroughly after applying changes.

---

## 📂 Author
- Created by **Mairazul Khan**
