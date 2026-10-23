# IoT-Shield

IoT-Shield is a manually provisioned, offline-installing Linux gateway designed to operate as a default-deny IPv4 firewall and security enforcement agent. 

## Overview
IoT-Shield runs on Linux systems equipped with standard native tools (`nftables`, `iproute2`, `libpcap`, and Python 3.10+ `venv`). By default, it performs no network downloads during installation, utilizing a completely embedded, SHA256-verified offline Python wheelhouse and metadata snapshot bundle.

## Key Features
* **Default-Deny Policy:** Unknown or un-enrolled devices are automatically blocked.
* **Fully Offline Installation:** Installs all pinned Python dependencies (`scapy`, `requests`, and transitive dependencies) directly from bundled wheels via local hashing.
* **Hardened Systemd Integration:** Generates and installs dedicated systemd services and guard scripts.
* **Passive Traffic Inspection:** Utilizes native `libpcap` and Scapy for monitoring without relying on active cloud telemetry.
* **Public Catalog Seeding:** Bundles IEEE OUI and CISA Known Exploited Vulnerabilities (KEV) snapshots for local analysis.

## Prerequisites
* Linux OS with root/sudo privileges (`CAP_NET_ADMIN`, `CAP_NET_RAW`).
* Python 3.10 or higher with `venv`.
* `nftables` (v1.0.6+) and `iproute2`.
* Native `libpcap` library.
* Pre-configured application home directory at `/var/lib/iot-shield` owned by `root:root` with `0700` permissions.

## Quick Start
1. Ensure the state directory is provisioned manually:
   ```bash
   sudo mkdir -p /var/lib/iot-shield
   sudo chown root:root /var/lib/iot-shield
   sudo chmod 0700 /var/lib/iot-shield
   Run the main installation script with root privileges:

Run the main installation script with root privileges:
sudo python3 -I /var/lib/iot-shield/IoT-Shield.py

To inspect bundled source files, wheels, and documentation without installing:
python3 IoT-Shield.py --extract-source /path/to/inspect
