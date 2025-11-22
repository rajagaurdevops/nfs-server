# 🗂️ NFS Setup Guide on AWS EC2

## 📌 Overview

This guide explains how to install, configure, and mount an NFS (Network File System) share between two EC2 instances in AWS — one acting as the **NFS Server** and the other as the **NFS Client**.

---

## 🚀 Why Use NFS?

While tools like `scp` let you copy files, they **do not provide shared storage**.  
NFS allows:

- Multiple servers to access the **same directory**
- Real-time shared storage for applications
- Shared web content (WordPress, Apache, etc.)
- Collaboration between distributed systems

NFS behaves like a shared network drive.

---

## 🔒 Private IP vs Public IP

NFS should run using **private IP addresses** inside AWS.

| Feature | Private IP | Public IP |
|---------|-----------|-----------|
| Visible on internet | ❌ No | ✅ Yes |
| Secure | ✅ Yes | ⚠️ Risky |
| Fast | ✅ Yes | ⚠️ Slower |
| Suitable for NFS | ✅ Recommended | ❌ Not Recommended |

👉 Use **Private IPs** because NFS is designed for internal networks, not public internet.

---

## 🏗️ Architecture

| Component | Role |
|----------|------|
| EC2 Instance #1 | NFS Server |
| EC2 Instance #2 | NFS Client |
| Network | Both instances in the same VPC |

---

## 🛠️ Step 1 — Install & Configure NFS Server

Run on the server:

```bash
sudo apt update
sudo apt install nfs-kernel-server -y
