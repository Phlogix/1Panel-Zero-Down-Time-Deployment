# 🚀 1Panel Zero Downtime Deployment via OneDev

## 🧩 Step 1: Install OneDev on 1Panel

Follow the instructions provided in this [GitHub issue](https://github.com/1Panel-dev/1Panel/issues/8974) to install OneDev using the Docker container method.

Once installed:

- Set up SSL certificates.
- Assign your custom domain (e.g., `onedev.youramazingdomain.com`).
- Create your admin credentials.
- Import all your project repositories from GitHub, GitLab, etc.

---

## 🔐 Step 2: Generate SSH Key on the OneDev Server

Login to the **1Panel** web portal.

Navigate to:  
**`Containers → OneDev-Container → Terminal → Connect`**

Run the following command to generate your SSH key:

```bash
ssh-keygen -t ed25519 -C "onedev-deploy-key"
```

After it's generated, copy your public key:

```bash
cat ~/.ssh/id_ed25519.pub
```

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
