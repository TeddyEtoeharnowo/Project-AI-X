---

# 🧑‍🏫 Tutorial: Give `newuser` SSH Access to Your Ubuntu Server Using PuTTY & Ed25519

---

## 🧰 On Windows (Client Side)

### Step 1: Install PuTTY & PuTTYgen  
- Download from [https://www.putty.org](https://www.putty.org)  
- Install both PuTTY and PuTTYgen on your Windows laptop.

### Step 2: Generate an Ed25519 Key  
1. Open **PuTTYgen**  
2. Under “Parameters” at the bottom:  
   - **Key type**: `EdDSA`  
   - **Curve**: `255` (for Ed25519)  
3. Click **Generate** and move your mouse randomly as prompted.  
4. *(Optional)* Add a passphrase for extra security.  
5. Save:  
   - The **private key** as a `.ppk` file  
   - The **public key** (copy from the top box)

### Step 3: Share the Public Key  
- Send the copied **public key** to the server admin (not the `.ppk` file).

---

## 🖥️ On Ubuntu (Server Side)

### Step 4: Create the New User  
Run:  
`adduser newuser`

### Step 5: Configure SSH Key Access  
1. Create the `.ssh` directory:  
   `mkdir /home/newuser/.ssh`

2. Add the public key:  
   `nano /home/newuser/.ssh/authorized_keys`  
   - Paste the key **from PuTTYgen’s top box**, starting with `ssh-ed25519`.

3. Set permissions:  
   `chmod 700 /home/newuser/.ssh`  
   `chmod 600 /home/newuser/.ssh/authorized_keys`  
   `chown -R newuser:newuser /home/newuser/.ssh`

### Step 6: Make Sure SSH Is Ready  
If using a custom port (e.g. `22`):  
`sudo ufw allow 22/tcp`  
`sudo systemctl restart ssh`

---

## 💻 Back on Windows (Client Side)

### Step 7: Open PuTTY  
- **Host Name**: `[server IP]` (e.g. `123.123.123.123`)  
- **Port**: `[port number]` (e.g. `22`)  
- **Connection Type**: `SSH`

### Step 8: Configure SSH Auth  
- Go to: `Connection → SSH → Auth`  
- Browse for and select the saved `.ppk` private key.

### Step 9: Set Username  
- Go to: `Connection → Data → Auto-login username`  
- Set it to: `newuser`

### Step 10: Connect!  
- Click **Open**  
- Accept the server fingerprint if prompted  
- If the key is accepted and setup is correct — ✅ `newuser` is logged in!

---

**ℹ️ After logging in for the first time, you should change your password on the server (the server admin set one for you):**  
Run:  
`passwd`
---
