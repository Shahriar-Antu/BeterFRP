# BetterFRP v1.0.0

First official release of **BetterFRP** — Enhanced Fast Reverse Proxy with Source IP Tracking Dashboard.

## ✨ Key Features
* **Modern Web Dashboard**: Vue 3 + TypeScript administrative console with real-time metrics for bandwidth, client connections, and proxy statuses.
* **Source IP Tracking**: Track remote client IP addresses connected to each active proxy with connection counts and color-coded activity badges (`HIGH`, `MEDIUM`, `LOW`).
* **Nil-Safe & Memory-Optimized Aggregation**: Thread-safe metric collection with auto-cleanup when HTTP or TCP connections terminate.

## 🚀 Core Functionality
* Supports **TCP**, **UDP**, **HTTP**, **HTTPS**, **STCP**, **SUDP**, **TCPMUX**, and **P2P** proxy modes.
* End-to-end TLS encryption, KCP & QUIC protocol transport, multiplexing, and authentication (Token & OIDC).
