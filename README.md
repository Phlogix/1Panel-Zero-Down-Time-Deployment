# 🚀 1Panel Zero Downtime Deployment via OneDev

## 🧩 Step 1: Install OneDev on 1Panel

Follow the instructions provided in this [GitHub issue](https://github.com/1Panel-dev/1Panel/issues/8974) to install OneDev using the Docker container method.

Once installed:

- Set up SSL certificates.
- Assign your custom domain (e.g., `onedev.youramazingdomain.com`).
- Create your admin credentials.
- Import all your project repositories from GitHub, GitLab, etc.

---

## 🔐 Step 2: Generate SSH Key on the OneDev Server Container

### 📥 1. Login to 1Panel

Open the 1Panel web portal, then navigate to:

**Containers → OneDev-Container → Terminal → Connect**

---

### 🔧 2. Generate an SSH Key

Run the following command in the terminal to create a new SSH key:

```bash
ssh-keygen -t ed25519 -C "your@email.com" -f ~/.ssh/onedev-container
```

---

### 🔃 3. Start the SSH Agent

```bash
eval "$(ssh-agent -s)"
```

---

### ➕ 4. Add Your SSH Key to the Agent

```bash
ssh-add ~/.ssh/onedev-container
```

---

### ⚙️ 5. Configure SSH Settings

Open the SSH config file:

```bash
nano ~/.ssh/config
```

Then add the following configuration:

```bash
Host your-onedev-url.com
    Port 2086  # Replace with your actual SSH port
    User onedev-container
    IdentityFile ~/.ssh/onedev-container
    IdentitiesOnly yes
```

---

### 🚀 6. Initialize Git Connection

Verify the SSH connection:

```bash
ssh -T your-onedev-url.com
```

---

### 📋 7. Copy Your Public SSH Key

Display the public key:

```bash
cat ~/.ssh/onedev-container.pub
```

---

### 🔑 8. Add the SSH Key to Your OneDev Account

1. Go to `your-onedev-url.com`
2. Click **Profile → SSH Keys**
3. Click the ➕ icon
4. Paste the copied SSH key
5. Save

---

### ✅ Congratulations!

Your OneDev container SSH key setup is complete.


Then go to your OneDev web interface:

- Click your **profile picture**.
- Go to **SSH KEYS**.
- Click the **plus (+)** icon and **paste** your SSH key.

---

## 🖥️ Step 3: Add Public Key to Your Deployment Target

Now let’s tell your deployment target server to allow OneDev access via SSH.

### On the Target Server:

1. Open your terminal (or use **1Panel shell**).
2. Edit the authorized keys file:

```bash
nano ~/.ssh/authorized_keys
```

3. Paste the contents of `id_ed25519.pub` (copied from OneDev).
4. Save and exit (`CTRL+X`, then `Y`, then `Enter`).

5. Set the correct file permissions:

```bash
chmod 700 ~/.ssh
chmod 600 ~/.ssh/authorized_keys
chown -R root:root ~/.ssh
```

---

## 🔍 Step 4: Check SSH Configuration on Target Server

Open your SSH config:

```bash
sudo nano /etc/ssh/sshd_config
```

Ensure the following lines exist and are **not commented out**:

```bash
PubkeyAuthentication yes
AuthorizedKeysFile .ssh/authorized_keys
PasswordAuthentication yes  # Optional fallback
```

Restart the SSH service to apply the changes:

```bash
sudo systemctl restart ssh
```

---

✅ You're now ready to set up **CI/CD pipelines** inside OneDev for **zero downtime deployment** to your servers running on 1Panel.
