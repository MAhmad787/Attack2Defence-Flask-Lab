# 🛡️ Wazuh SIEM Lab: Full Lifecycle Security Implementation

## 🧠 What is Wazuh?

Wazuh is a widely used, free and open-source platform that provides XDR (Extended Detection and Response) and SIEM (Security Information and Event Management) capabilities.

It supports a wide range of deployment options — containers, cloud environments, traditional hosts, and even agentless devices like firewalls, switches, and routers.

### Key Features:
- Log monitoring
- Threat detection
- Incident response and forensics
- Regulatory compliance
- Rule-based automation

---

## 🔧 Wazuh Components

### 📦 Wazuh Indexer
- Stores logs and alerts generated by the Wazuh server.
- Acts as a search and analytics engine.
- Supports filtering and full-text search.



---

### 🧠 Wazuh Server
- Core engine that processes data from agents, network devices, APIs, etc.
- Applies rulesets to detect anomalies and generate alerts.



---

### 📊 Wazuh Dashboard
- Visual interface showing real-time data via graphs, charts, and tables.
- Displays logs and alerts in a clean, readable format.



---

### 💻 Wazuh Agent
- Lightweight agent installed on endpoints.
- Collects logs, telemetry, and system data.
- Works across multiple OS platforms.



---

## 🚀 Installing the Wazuh Server

Wazuh has simple documentation and supports quick installation — perfect for labs or small setups.

### 🔧 Hardware Requirements (Minimal)

* 1–2 vCPU
* 2–4+ GiB RAM
* Disk space: depends on usage

For learning or lab purposes, you can run it on a VM with lower specs.

### ✅ Installation Steps

**Step 1: Download the Wazuh installer**

```bash
curl -sO https://packages.wazuh.com/4.12/wazuh-install.sh
```

**Step 2: Run the installer**

```bash
sudo bash ./wazuh-install.sh -a
```

☕ Grab a coffee, this might take a few minutes.

**Step 3: Extract login credentials**

```bash
sudo tar -O -xvf wazuh-install-files.tar wazuh-install-files/wazuh-passwords.txt
```

**Step 4: Access the Wazuh Dashboard**
Open a browser and navigate to:

```
https://<VM_IP_ADDRESS>
```

Use credentials from the extracted file.



---

## 💻 Installing Wazuh Agent on Ubuntu Endpoint

**Step 1: Import GPG Key**

```bash
curl -s https://packages.wazuh.com/key/GPG-KEY-WAZUH | gpg --no-default-keyring --keyring gnupg-ring:/usr/share/keyrings/wazuh.gpg --import && chmod 644 /usr/share/keyrings/wazuh.gpg
```

**Step 2: Add Wazuh repository**

```bash
echo "deb [signed-by=/usr/share/keyrings/wazuh.gpg] https://packages.wazuh.com/4.x/apt/ stable main" | tee -a /etc/apt/sources.list.d/wazuh.list
```

**Step 3: Update package list**

```bash
apt-get update
```

**Step 4: Install the agent**

```bash
apt-get install wazuh-agent
```

📝 **Note**: Ensure the agent version is equal to or lower than the server for compatibility. You may disable updates afterward.



---

## 🔗 Linking the Wazuh Agent with the Server

### 🛠️ Step 1: Configure Agent’s `ossec.conf`

Edit:

```bash
sudo nano /var/ossec/etc/ossec.conf
```

Add inside the `<client>` block:

```xml
<client>
  <server>
    <address>YOUR_WAZUH_SERVER_IP</address>
    <port>1514</port>
    <protocol>tcp</protocol>
  </server>
</client>
```



---

### 🛠️ Step 2: Add Agent on the Server

On server:

```bash
sudo /var/ossec/bin/manage_agents
```

* Press `A` to add a new agent.
* Enter agent name and IP.
* Copy the generated key.



---

### 🛠️ Step 3: Import Key on the Agent

On the agent system:

```bash
sudo /var/ossec/bin/manage_agents
```

* Press `I` to import a key.
* Paste the key copied from the server.



---

### 🛠️ Step 4: Restart Wazuh Agent

```bash
sudo systemctl restart wazuh-agent
```

---

### ✅ Verify Connection

Log into the Wazuh Dashboard and confirm the agent is active.



