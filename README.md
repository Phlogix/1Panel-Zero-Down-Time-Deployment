# 🚀 1Panel Zero Downtime Deployment via OneDev

## 🧠 What is 1Panel?

[1Panel](https://github.com/1Panel-dev/1Panel) is a modern, open-source server management panel designed for simplicity, efficiency, and ease of use. It allows you to manage Linux servers and deploy web applications via a user-friendly web interface. With support for Docker, domain binding, SSL certificates, and multiple app templates, 1Panel is perfect for developers, startups, and sysadmins looking to streamline server management.

## 🛠️ What is OneDev?

[OneDev](https://github.com/theonedev/onedev) is an all-in-one DevOps platform that provides Git repository hosting, CI/CD pipelines, issue tracking, code review, and a powerful self-hosted development workflow. Think of it as a private GitHub + GitLab + Jenkins combo, ideal for teams or solo developers who want full control over their infrastructure.

## 🤝 Why use OneDev with 1Panel?

By deploying OneDev via 1Panel, you get the best of both worlds:
- **1Panel** handles server and Docker container management with SSL and domain integration.
- **OneDev** manages your codebase, automates deployments, and provides developer tools—all in a private, secure environment.

This guide walks you through deploying OneDev on your server using 1Panel with **zero downtime** and optimal configuration.

---

<p align="center">
  <a href="https://your-destination-url.com" target="_blank">
    <img src="https://raw.githubusercontent.com/Devinsomnia/ads/main/PNG/wittyai.png" alt="WittyAI" width="150" height="150">
  </a>
</p>

<p align="center">
  <strong>WittyAi was here</strong>
</p>

---

## 🧩 Step 1: Install OneDev on 1Panel

Follow the instructions provided in this [GitHub issue](https://github.com/1Panel-dev/1Panel/issues/8974) to install OneDev using the Docker container method.

Once installed:

- Set up SSL certificates.
- Assign your custom domain (e.g., `onedev.youramazingdomain.com`).
- Create your admin credentials.
- Import all your project repositories from GitHub, GitLab, etc.

---

<p align="center">
  <a href="https://your-destination-url.com" target="_blank">
    <img src="https://raw.githubusercontent.com/Devinsomnia/ads/main/PNG/wittyai.png" alt="WittyAI" width="150" height="150">
  </a>
</p>

<p align="center">
  <strong>WittyAi was here</strong>
</p>

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
Host onedev.youramazingdomain.com
    Port 2086  # Replace with your actual SSH port
    User onedev-container
    IdentityFile ~/.ssh/onedev-container
    IdentitiesOnly yes
```

---

### 🚀 6. Initialize Git Connection

Verify the SSH connection:

```bash
ssh -T onedev.youramazingdomain.com
```

---

### 📋 7. Copy Your Public SSH Key

Display the public key:

```bash
cat ~/.ssh/onedev-container.pub
```

---

### 🔑 8. Add the SSH Key to Your OneDev Account

1. Go to `onedev.youramazingdomain.com`
2. Click **Profile → SSH Keys**
3. Click the ➕ icon
4. Paste the copied SSH key
5. Save

---

### 🔑 9. Clone your repo without auth through your key

`Do not forget to update your port`

```bash
git clone ssh://onedev.youramazingdomain.com:2086/your-amazing-repo
```

---

### ✅ Congratulations!

Your OneDev container SSH key setup is complete.

---

<p align="center">
  <a href="https://your-destination-url.com" target="_blank">
    <img src="https://raw.githubusercontent.com/Devinsomnia/ads/main/PNG/wittyai.png" alt="WittyAI" width="150" height="150">
  </a>
</p>

<p align="center">
  <strong>WittyAi was here</strong>
</p>

---

## 🔐 Step 3: Generate SSH Key on the Device where will you make development

### 📥 1. Login to 1Panel

Open the 1Panel web portal, then navigate to:

**Containers → OneDev-Container → Terminal → Connect**

---

### 🔧 2. Generate an SSH Key

Run the following command in the terminal to create a new SSH key:

```bash
ssh-keygen -t ed25519 -C "your@email.com" -f ~/.ssh/development-pc
```

---

### 🔃 3. Start the SSH Agent

```bash
eval "$(ssh-agent -s)"
```

---

### ➕ 4. Add Your SSH Key to the Agent

```bash
ssh-add ~/.ssh/development-pc
```

---

### ⚙️ 5. Configure SSH Settings

Open the SSH config file:

```bash
nano ~/.ssh/config
```

Then add the following configuration:

```bash
Host onedev.youramazingdomain.com
    Port 2086  # Replace with your actual SSH port
    User development-pc
    IdentityFile ~/.ssh/development-pc
    IdentitiesOnly yes
```

---

### 🚀 6. Initialize Git Connection

Verify the SSH connection:

```bash
ssh -T onedev.youramazingdomain.com
```

---

### 📋 7. Copy Your Public SSH Key

Display the public key:

```bash
cat ~/.ssh/development-pc.pub
```

---

### 🔑 8. Add the SSH Key to Your OneDev Account

1. Go to `onedev.youramazingdomain.com`
2. Click **Profile → SSH Keys**
3. Click the ➕ icon
4. Paste the copied SSH key
5. Save

---

### 🔑 9. Clone your repo without auth through your key

`Do not forget to update your port`

```bash
git clone ssh://onedev.youramazingdomain.com:2086/your-amazing-repo
```

---

### ✅ Congratulations!

Your Development PC's SSH key setup is complete.

---

<p align="center">
  <a href="https://your-destination-url.com" target="_blank">
    <img src="https://raw.githubusercontent.com/Devinsomnia/ads/main/PNG/wittyai.png" alt="WittyAI" width="150" height="150">
  </a>
</p>

<p align="center">
  <strong>WittyAi was here</strong>
</p>

---

## 🔐 Step 4: Set the Agent on Your 1Panel Server

### 🧭 1. Navigate to OneDev Dashboard

1. Go to `onedev.youramazingdomain.com`
2. Go to **Administration → Agents → ➕ (Plus Icon)**  
3. Select the tab **Run on Bare Metal / Virtual Machine**
4. Download either `agent.zip` or `agent.tar.gz`

---

### 🖥️ 2. SSH into Your Server

Make sure you are logged in with root privileges.

---

### 🔑 3. Create Folder for Your Agent

```bash
mkdir -p /opt/onedev-agent
```

---

### 📁 4. Upload & Extract Agent Files

1. Connect to your server using your preferred FTP application  
2. Navigate to: `/opt/onedev-agent`  
3. Upload and extract `agent.zip` or `agent.tar.gz`  
4. Ensure the contents are located in `/opt/onedev-agent`

---

### 🧾 5. Make the Agent Script Executable

```bash
chmod +x bin/agent.sh
```

---

<p align="center">
  <a href="https://your-destination-url.com" target="_blank">
    <img src="https://raw.githubusercontent.com/Devinsomnia/ads/main/PNG/wittyai.png" alt="WittyAI" width="150" height="150">
  </a>
</p>

<p align="center">
  <strong>WittyAi was here</strong>
</p>

---

## 🔐 Step 5: Create a Linux Service for the OneDev Agent

### 🛠️ 1. Create the Service File

```bash
sudo nano /etc/systemd/system/onedev.service
```

---

### 📝 2. Add the Following Content

```ini
[Unit]
Description=OneDev Agent Service
After=network.target

[Service]
Type=simple
User=root
WorkingDirectory=/opt/onedev-agent
ExecStart=/opt/onedev-agent/bin/agent.sh start
ExecStop=/opt/onedev-agent/bin/agent.sh stop
Restart=always
RestartSec=5
StandardOutput=syslog
StandardError=syslog
SyslogIdentifier=onedev-agent

[Install]
WantedBy=multi-user.target
```

> Press `Ctrl + X`, then press `Y` to save and exit.

---

### 🔄 3. Reload the Daemon

```bash
sudo systemctl daemon-reload
```

---

### ▶️ 4. Start the Service

```bash
sudo systemctl start onedev
```

---

### 📌 5. Enable the Service on Boot

```bash
sudo systemctl enable onedev
```

---

### 📊 6. Check Service Status

```bash
sudo systemctl status onedev
```

---

### 🖥️ 7. Verify Agent in OneDev

1. Go to `onedev.youramazingdomain.com`
2. Navigate to **Administration → Agents**
3. Your agent should appear with your server's **hostname**, **IP address**, and **Status: Online**

---

### ✅ Congratulations!

You’ve successfully completed the **OneDev Agent Setup** on your server! 🚀

---

<p align="center">
  <a href="https://your-destination-url.com" target="_blank">
    <img src="https://raw.githubusercontent.com/Devinsomnia/ads/main/PNG/wittyai.png" alt="WittyAI" width="150" height="150">
  </a>
</p>

<p align="center">
  <strong>WittyAi was here</strong>
</p>

---

## 🔐 Step 5: Create a Job Executor on OneDev
1. Go to `onedev.youramazingdomain.com`
2. Navigate to **Administration → Job Executor**
3. Click **Add Executor**
4. Choose **Remote Sheel Executor**
5. Give a name like **deploy, deployment, zero-down-time-deployment**
6. Set your agent selector theme like this **"Name" is "Your Server's Hostname"** you will be able to choose your server hostname there it is automatically fetch that info from the agent section.
7. Click **Test**
8. test it with

```bash
/opt/onedev-agent
```

9. You must see the response **Job executor tested successfully**
10. Save the Job Executor 

---

<p align="center">
  <a href="https://your-destination-url.com" target="_blank">
    <img src="https://raw.githubusercontent.com/Devinsomnia/ads/main/PNG/wittyai.png" alt="WittyAI" width="150" height="150">
  </a>
</p>

<p align="center">
  <strong>WittyAi was here</strong>
</p>

---

## 🔐 Step 6: create necessary folder paths such as temp-git and overlays for your websites

```bash
mkdir -p your-1Panel-folder-path/apps/temp-git
```

and

```bash
mkdir -p your-1Panel-folder-path/apps/overlays 
```

**Use overlays folder for your development environment and production envriment files which needs replaced after cloning**

---

<p align="center">
  <a href="https://your-destination-url.com" target="_blank">
    <img src="https://raw.githubusercontent.com/Devinsomnia/ads/main/PNG/wittyai.png" alt="WittyAI" width="150" height="150">
  </a>
</p>

<p align="center">
  <strong>WittyAi was here</strong>
</p>

---

## 🔐 Step 7: create necessary folder paths such as temp-git and overlays for your websites

1. Go to `onedev.youramazingdomain.com`
2. Navigate to **Projects → Choose your amazing repo**
3. Create **.onedev-buildspec.yml**
4. Click  **Add new**
5. Name it **Deploy to Server**
6. On the section of Job Executor write your job executor name which did you named previously **deploy, deployment, zero-down-time-deployment**
7. Come to the steps section press plus icon
8. Search for execute commands and choose it 
9. Give a name you can use your repo's name
10. Disable run in container
11. Interpreter must be selected default
12. Condition must be selected successful
13. Add your codes in Commands section find the example setup below

```bash
#!/bin/bash

echo "🚀 Zero Downtime Deployment has started..."

# === CONFIGURATION ===
TEMP_DIR="your-1Panel-folder-path/apps/temp-git"
REPO_NAME="your-amazing-repo"
TIMESTAMP=$(date +"%Y%m%d-%H%M%S")
CLONE_DIR="$TEMP_DIR/${REPO_NAME}-${TIMESTAMP}"
TARGET_DIR="your-1Panel-folder-path/apps/openresty/openresty/www/sites/your-amazing-website.com/index"
REPO_URL="ssh://onedev.youramazingdomain.com:2086/your-amazing-repo"
MAX_VERSIONS=3

# === ENSURE TEMP DIR EXISTS ===
echo "📁 Ensuring temp directory exists: $TEMP_DIR"
mkdir -p "$TEMP_DIR"

# === CLONE REPO WITH TIMESTAMP ===
echo "📥 Cloning into: $CLONE_DIR"
git clone --depth=1 "$REPO_URL" "$CLONE_DIR"

# === VERIFY CLONE SUCCESS ===
if [ ! -d "$CLONE_DIR" ]; then
  echo "❌ Clone failed. Aborting deployment."
  exit 1
fi

# === REMOVE UNWANTED DOTFILES FROM TARGET (KEEP .env) ===
echo "🧹 Removing unwanted hidden files from live directory (excluding .env)..."

# Remove dotfiles (files) except .env
find "$TARGET_DIR" -maxdepth 1 -type f -name ".*" ! -name ".env" -exec rm -f {} \;

# Remove dotfolders (directories) except .env (not needed if .env is a file)
find "$TARGET_DIR" -maxdepth 1 -type d -name ".*" ! -name "." ! -name ".." ! -name ".env" -exec rm -rf {} \;


# === SYNC TO LIVE DIRECTORY (EXCLUDE DOTFILES FROM SOURCE) ===
echo "📂 Syncing clean files to live directory..."
rsync -av --delete \
  --exclude='.*' \
  --exclude='*/.git/' \
  "$CLONE_DIR"/ "$TARGET_DIR"/

# === CLEANUP OLD CLONES (KEEP ONLY LAST 3) ===
echo "🗑️ Checking for old versions to delete..."
cd "$TEMP_DIR" || exit 1

ls -dt ${REPO_NAME}-* 2>/dev/null | tail -n +$((MAX_VERSIONS + 1)) | while read -r old_dir; do
  echo "🗑️ Removing old clone: $TEMP_DIR/$old_dir"
  rm -rf "$TEMP_DIR/$old_dir"
done

# === DONE ===
echo "🎉 Deployment completed successfully to: $TARGET_DIR"

```

## 🏁 Final Result

By completing this setup, you've established a **secure, scalable, and self-hosted CI/CD environment** using **1Panel** and **OneDev**.

Your organization now benefits from:

- ✅ **Zero-downtime deployments** — ensure continuous service availability without disrupting users.
- 🔐 **Full control over your source code and pipelines** — enhance codebase security and meet compliance standards.
- 💸 **Significant cost savings** — eliminate reliance on expensive third-party CI/CD platforms, saving thousands annually.
- 🚀 **Scalable DevOps workflow** — customize and grow your infrastructure on your terms.

This setup gives your team the power to ship faster, safer, and smarter—without vendor lock-in.

---

<p align="center">
  <a href="https://your-destination-url.com" target="_blank">
    <img src="https://raw.githubusercontent.com/Devinsomnia/ads/main/PNG/wittyai.png" alt="WittyAI" width="150" height="150">
  </a>
</p>

<p align="center">
  <strong>WittyAi was here</strong>
</p>

---

## 📬 Enterprise Consulting & Support

Need a robust, secure CI/CD environment tailored to your organization's needs? 

We offer **enterprise consulting**, including:

- Custom CI/CD pipeline design (leveraging Agile methodologies and systems engineering expertise)
- Secure infrastructure setup (certified in data protection, EU/UK GDPR, and TS EN 50600 standards)
- Advanced networking integration (expertise in complex network design and management)
- Big data & analytics optimization (skilled in managing and analyzing large datasets)
- Leadership & team enablement (support with communication, mentoring, and collaboration strategies)
- Version control solutions (proficient in Git and GitHub for effective code management)

📩 **Contact us:**  
For pricing and consultation based on your specific requirements, reach out to:

**devinsomnia@wittyai.co.uk**



