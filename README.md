<p align="center">
  <img src="assets/Q-TEAM.png" width="200">
</p>

<p align="center">
  <a href="./releases">
    <img src="https://img.shields.io/badge/RELEASES-v1.0.0-blue.svg" alt="Release">
  </a>
  &nbsp;&nbsp;&nbsp;
  <a href="https://github.com/Qteam-official/ICMPTunnel/blob/main/LICENSE">
    <img src="https://img.shields.io/badge/LICENSE-Q T E A M-red.svg" alt="License">
  </a>
   &nbsp;&nbsp;&nbsp;
  <a href="https://t.me/Qteam_official">
    <img src="https://img.shields.io/badge/Telegram-Q T E A M-green.svg" alt="Telegram">
  </a>
</p>



---

# ICMPTunnel

**ICMPTunnel** is a proprietary binary tool developed by **Q-TEAM**.  
It demonstrates tunneling over the ICMP protocol (commonly used by ping).


---

## 🛠️ How to Use

### 📥 Installer ( Recommended )

1. Just run this command to download and start :

```bash
bash <(curl -Ls https://raw.githubusercontent.com/Qteam-official/ICMPTunnel/main/install.sh)
```

2. Then type
```bash
q-icmp
```

### 📦 Offline Installation (Internet restrictions)

If you want to install ICMPTunnel without downloading from GitHub (for example, in an offline environment), follow these steps:

1. **Download the latest release binary** (`ICMPTunnel`) from the [Releases page](https://github.com/Qteam-official/ICMPTunnel/releases) using another computer with internet access.
2. **Copy** both `install.sh` and the downloaded `ICMPTunnel` binary to your target (offline) Linux machine, placing them in the same directory.
3. **Make sure both files are executable:**

```bash
chmod +x install.sh ICMPtunnel
```

4. **Run the installer:**

```bash
sudo ./install.sh
```

5. When prompted, select `2` for **Offline Installation**.
6. Follow the interactive prompts to choose Client or Server mode and complete the setup.

After installation, you can manage the tunnel using:

```bash
q-icmp
```

> **Note:** The binary file must be named exactly `ICMPTunnel` and be in the same directory as `install.sh` during installation.

### 🚢 Install With Docker Compose

1. **Install Docker** using the official installation script:

```bash
curl -fsSL https://get.docker.com | sh
```

2. Make a new working directory and download the latest `Dockerfile`:

```bash
mkdir ICMPTunnel && cd ICMPTunnel
curl --output Dockerfile "https://raw.githubusercontent.com/sepehrmoh81/ICMPTunnel/main/docker/Dockerfile"
```

3. Create the proper docker compose configuration.

- Open `docker-compose.yml` in your favorite editor (e.g. nano):

```bash
nano docker-compose.yml
```

- Copy&Paste the proper configuration (server/client) and save. (`ctrl + x`, `y` and `enter` for nano)

#### Server Mode:
```yaml
services:
  icmptunnel-server:
    build: .
    container_name: icmptunnel-server
    restart: unless-stopped
    network_mode: host
    privileged: true
    cap_add:
      - NET_ADMIN
      - NET_RAW
    command: ["/usr/local/bin/ICMPTunnel", "-type", "server"]
    healthcheck:
      test: ["CMD", "pgrep", "-x", "ICMPTunnel"]
      interval: 30s
      timeout: 10s
      retries: 3
      start_period: 5s
```

#### Client Mode:
```yaml
services:
  icmptunnel-client:
    build: .
    container_name: icmptunnel-client
    restart: unless-stopped
    network_mode: host
    privileged: true
    cap_add:
      - NET_ADMIN
      - NET_RAW
    ports:
      - "1010:1010"
    environment:
      - SERVER_IP=${SERVER_IP:-127.0.0.1}
    command: ["/usr/local/bin/ICMPTunnel", "-type", "client", "-l", ":1010", "-s", "${SERVER_IP:-127.0.0.1}", "-sock5", "1"]
    healthcheck:
      test: ["CMD", "pgrep", "-x", "ICMPTunnel"]
      interval: 30s
      timeout: 10s
      retries: 3
      start_period: 5s
```

4. **⚠️CLIENT MODE ONLY:** Create a `.env` file to store server IP:

- Open `.env` in your favorite editor (e.g. nano):

```bash
nano .env
```

- Copy&Paste the following, replace 127.0.0.1 with your **SERVER IP** and save. (`ctrl + x`, `y` and `enter` for nano)

```shell
# ICMPTunnel Client Configuration
# Set the server IP address where the ICMPTunnel server is running
SERVER_IP=127.0.0.1
```

5. **Run** ICMPTunnel container:

```bash
docker compose up -d
```

6. **Check** the logs:

```bash
docker compose logs
```

---


# ✅ Supported Platforms:

+ Linux (amd64, arm64, arm, 386)
+ Windows (amd64, 386)
+ macOS (darwin-amd64, darwin-arm64)

# ✅ Tested on :

+ 🐧 Ubuntu 18.04, 20.04, 22.04+
+ 🐧 Debian 10/11/12+
+ 🐧 Kali, Mint, Fedora, CentOS, AlmaLinux, Rocky
+ 🐧 Arch, Manjaro, openSUSE
+ 🐧 Pop!_OS, Zorin OS, and other modern distros
+ 🪟 Windows 10/11 (both 64-bit and 32-bit)
+ 🍎 macOS (Intel & Apple Silicon)

---

### Ensure ICMP (ping) is allowed on both sides (no firewall blocks)
### Root is NOT required in most modern systems
### No ports need to be opened manually — it works via ICMP!

---


## 🧱 Binary Distribution

This repository contains the official binary release of **ICMPTunnel**, developed by **Q-TEAM**.

It is provided as a ready-to-use executable with no additional components.

---

## 🚫 Usage Restrictions

This binary is the **intellectual property of Q-TEAM**.

You are **not allowed** to:
- Copy or redistribute this binary
- Modify or reverse engineer it
- Use it for unauthorized or illegal purposes

without **explicit written permission** from Q-TEAM.


---


## ⚠️ Disclaimer

ICMP-based tunneling may be restricted on some networks.  
Use of this tool is limited to **legal, educational, or testing purposes in controlled environments only**.

**Q-TEAM is not responsible for any misuse of this software.**

---

## 📈 Star History

[![Star Chart](https://api.star-history.com/svg?repos=Qteam-official/ICMPTunnel&type=Date&theme=dark)](https://star-history.com/#Qteam-official/ICMPTunnel&Date)

> Growth of the community over time 🚀 — Thank you for every ⭐!


---

© 2025 Q-TEAM. All rights reserved.
