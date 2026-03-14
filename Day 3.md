# Security Hardening: Restricting Direct Root SSH Login

### KodeKloud – 100 Days of DevOps Challenge

---

## 📌 Project Overview

As part of the security audit protocols for **xFusionCorp Industries**, the security team mandated the restriction of **direct root SSH logins** across all application servers in the **Stratos Datacenter**.

The goal is to:

* Reduce the risk of **brute-force attacks** targeting the root account
* Ensure administrative actions are performed through **identifiable user accounts** with escalated privileges
* Maintain a **secure and auditable environment** for server management

This task focuses on **hardening Linux servers** by updating SSH configurations.

---

## 🏗️ Infrastructure Details

| Server Name  | Hostname                        | User   | IP Address    |
| ------------ | ------------------------------- | ------ | ------------- |
| App Server 1 | stapp01.stratos.xfusioncorp.com | tony   | 172.16.238.10 |
| App Server 2 | stapp02.stratos.xfusioncorp.com | steve  | 172.16.238.11 |
| App Server 3 | stapp03.stratos.xfusioncorp.com | banner | 172.16.238.12 |

---

## 🔐 Why Restrict Root SSH Login

Direct root login poses several security risks:

* Easy target for **brute-force attacks**
* Lack of **accountability** since all actions appear under the root user
* Violates **best practices for privilege management**

Using regular users with **`sudo` privileges** ensures:

* Administrative actions are **logged and traceable**
* Access can be **controlled and revoked per user**
* Overall server security posture is **improved**

---

## 🧰 Tools & Commands Used

| Command                  | Description                                     |
| ------------------------ | ----------------------------------------------- |
| `ssh`                    | Connect to remote servers                       |
| `sudo`                   | Execute commands with administrative privileges |
| `vi` or `nano`           | Edit configuration files                        |
| `systemctl restart sshd` | Apply SSH configuration changes                 |
| `grep`                   | Verify SSH configuration settings               |

---

## 💻 Implementation Steps

### Step 1: Connect to the Target Server

Use SSH to connect as a non-root user:

```bash
ssh tony@172.16.238.10
```

---

### Step 2: Edit SSH Configuration

Open the SSH daemon configuration file:

```bash
sudo vi /etc/ssh/sshd_config
```

Locate the directive:

```text
#PermitRootLogin yes
```

Change it to:

```text
PermitRootLogin no
```

> This setting **disables direct root SSH access**.

---

### Step 3: Apply Configuration Changes

Restart the SSH service to apply the updated configuration:

```bash
sudo systemctl restart sshd
```

Verify the configuration has been applied:

```bash
sudo grep PermitRootLogin /etc/ssh/sshd_config
```

Expected output:

```text
PermitRootLogin no
```

---

### Step 4: Test SSH Access

1. Attempt to login directly as root:

```bash
ssh root@172.16.238.10
```

2. The connection should be **refused**, confirming that root login is disabled.

3. Login using a regular user and escalate privileges via `sudo` to perform administrative tasks.

---

## ✅ Result

* Direct root SSH login is **disabled on all application servers**
* Administrative access is now performed via **user accounts with `sudo` privileges**
* Server hardening aligns with **security best practices** and audit requirements

---

## 🔎 Best Practices for SSH Security

* Disable **root login** and use **sudo-enabled users**
* Implement **SSH key-based authentication**
* Use **strong passwords** for all accounts
* Regularly audit **user access and login attempts**
* Consider **fail2ban** or other intrusion prevention tools for added security

These practices help maintain **secure, auditable, and manageable infrastructure**.

---

## 📚 Learning Outcome

From completing this task, the following skills were reinforced:

* SSH configuration management (`/etc/ssh/sshd_config`)
* Server hardening and security best practices
* Using `sudo` for privileged access
* Testing and validating configuration changes
* Understanding **principle of least privilege** in Linux environments

---

## 🚀 Part of

**KodeKloud – 100 Days of DevOps Challenge**

Focus areas include:

* Linux Administration
* Security Hardening
* Networking
* Containers and Kubernetes
* Automation

---

## 👨‍💻 Author

DevOps Learner participating in the **KodeKloud 100 Days of DevOps Challenge**

---

If you want, I can **also combine Day 2 and Day 3 into a single polished portfolio README** with badges, visual highlights, and consistent formatting—so it looks professional for GitHub recruiters.

Do you want me to do that next?
