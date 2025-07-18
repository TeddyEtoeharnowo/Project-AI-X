---

# 🧑‍🏫 Tutorial: Give `[username]` SSH Access to Your Ubuntu Server Using PuTTY

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
`adduser [username]`

### Step 5: Configure SSH Key Access  
1. Create the `.ssh` directory:  
   `mkdir /home/[username]/.ssh`

2. Add the public key:  
   `nano /home/[username]/.ssh/authorized_keys`  
   - Paste the key **from PuTTYgen’s top box**, starting with `ssh-ed25519`.

3. Set permissions:  
   `chmod 700 /home/[username]/.ssh`  
   `chmod 600 /home/[username]/.ssh/authorized_keys`  
   `chown -R [username]:[username] /home/[username]/.ssh`

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
- Set it to: `[username]`

### Step 10: Connect!  
- Click **Open**  
- Accept the server fingerprint if prompted  
- If the key is accepted and setup is correct — ✅ `[username]` is logged in!

---

## 🔒 Important Security Reminders

- **Change your password after first login:**  
  The server admin set an initial password for you. Change it by running:  
  `passwd`
  
- **Never connect to the server on unsecured WiFi!**  
  Only use trusted, password-protected networks. Public or open WiFi can expose your connection to attackers. Use a VPN if you have to.

- **Never share your private key (`.ppk` file) or your password with anyone.**  
  Only share your public key if needed.

- **Keep your private key safe:**  
  Store it in a secure location on your computer. If someone else gets your private key, they can access your account.

- **Use a strong passphrase for your private key if possible.**  
  This adds an extra layer of protection.

- **Be careful with copy-pasting commands:**  
  Only run commands you understand or that are from trusted sources.

- **Log out when you’re done:**  
  Always close your SSH session when you’re finished.

- **If you think your account or key is compromised, tell your admin immediately.**

---
