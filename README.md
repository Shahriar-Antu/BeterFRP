# BetterFRP ⚡

[![Go Version](https://img.shields.io/badge/Go-1.22%2B-00ADD8?style=flat&logo=go)](https://golang.org)
[![Vue 3](https://img.shields.io/badge/Vue-3.x-4FC08D?style=flat&logo=vuedotjs)](https://vuejs.org/)
[![TypeScript](https://img.shields.io/badge/TypeScript-5.x-3178C6?style=flat&logo=typescript)](https://www.typescriptlang.org/)
[![License](https://img.shields.io/badge/License-Apache_2.0-blue.svg)](LICENSE)

**BetterFRP** is a high-performance, feature-rich reverse proxy built on top of [fatedier/frp](https://github.com/fatedier/frp). It enables you to securely expose local servers situated behind NATs or firewalls to the public Internet, enhanced with a modern **Vue 3 Web Dashboard** and **Real-Time Source IP Tracking**.

---

## ✨ Key Features & Enhancements

Beyond standard FRP capabilities, **BetterFRP** introduces powerful server management features:

* 📊 **Enhanced Web Dashboard (Vue 3 + TypeScript)**
  - Redesigned, glassmorphic dark-mode web console embedded directly into `frps`.
  - Live metric visualization for overall bandwidth, active proxy connections, and client daemons.
* 🔍 **Real-Time Connected Source IP Tracking**
  - Track and monitor the exact remote source IP addresses connecting to each active proxy.
  - View live connection counts per IP with activity indicators (**HIGH**, **MEDIUM**, **LOW**).
  - Memory-safe, thread-safe, and auto-cleaning on connection termination.
* ⚡ **Complete Protocol Support**
  - **TCP**, **UDP**, **HTTP**, **HTTPS**, **STCP** (Secret TCP), **SUDP** (Secret UDP), and **TCPMUX**.
  - P2P direct connection mode for low-latency point-to-point data transfers.
* 🔒 **Enterprise-Grade Security & Transport**
  - Multi-layer authentication: Token-based & OpenID Connect (OIDC).
  - TLS encryption, KCP protocol support, QUIC protocol support, and stream multiplexing (yamux).

---

## 🖥️ BetterFRP Dashboard Preview

The built-in web dashboard provides real-time visibility into all active reverse proxies and connected remote client IPs:

```
+-----------------------------------------------------------------------------------+
|  BetterFRP Server Dashboard                                 [User: admin]         |
+-----------------------------------------------------------------------------------+
|  [ Total Traffic ]           [ Active Connections ]         [ Connected Clients ] |
|  In: 1.2 TB / Out: 894 GB    78                             12                    |
+-----------------------------------------------------------------------------------+
| Proxy Details                                                                     |
| Active         Type     Port    Status    Traffic     Connected IPs Panel         |
| web-http       HTTP     8080    ONLINE    1.1 TB      IP Address      Conns  Level|
| ssh-tcp        TCP      2222    ONLINE    250 GB      192.168.1.45    18     HIGH |
| api-service    HTTP     8000    ONLINE    30 GB       10.0.0.12       9      MED  |
|                                                       172.16.0.88     5      LOW  |
+-----------------------------------------------------------------------------------+
```

---

## 🚀 Quick Start

### 1. Build from Source

Ensure you have **Go 1.22+** and **Node.js 18+** installed:

```bash
# Clone the repository
git clone https://github.com/Shahriar-Antu/BeterFRP.git
cd BeterFRP/beterfrp

# Build the Web Dashboard assets (Vue 3)
make web

# Build frps (Server) and frpc (Client) binaries
make build
```

The compiled binaries will be located in `./bin/frps` and `./bin/frpc`.

---

### 2. Configure & Run Server (`frps`)

Create a configuration file `frps.toml`:

```toml
bindPort = 7000

# Enable Web Dashboard
webServer.addr = "0.0.0.0"
webServer.port = 7500
webServer.user = "admin"
webServer.password = "admin"
```

Start the BetterFRP server:

```bash
./bin/frps -c ./frps.toml
```

Access the dashboard at `http://<SERVER_IP>:7500`.

---

### 3. Configure & Run Client (`frpc`)

Create a configuration file `frpc.toml` on your local machine:

```toml
serverAddr = "x.x.x.x"
serverPort = 7000

# Expose a local Web Server (HTTP)
[[proxies]]
name = "web-http"
type = "http"
localIP = "127.0.0.1"
localPort = 8080
customDomains = ["web.yourdomain.com"]

# Expose local SSH (TCP)
[[proxies]]
name = "ssh-tcp"
type = "tcp"
localIP = "127.0.0.1"
localPort = 22
remotePort = 2222
```

Start the BetterFRP client:

```bash
./bin/frpc -c ./frpc.toml
```

---

## 🛠️ Development & Testing

```bash
# Run unit tests
make test

# Run code formatters & linters
make fmt
make vet

# Clean up built artifacts
make clean
```

---

## 📄 License

BetterFRP is licensed under the [Apache 2.0 License](LICENSE).
