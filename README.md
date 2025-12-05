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

👉 Use **AWS EC2 instances inside the same VPC (or via VPN / VPC Peering) should always use private IP addresses when mounting NFS.
NFS is not designed for insecure or public internet connections.

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

``
sudo apt update
sudo apt install nfs-kernel-server -y



