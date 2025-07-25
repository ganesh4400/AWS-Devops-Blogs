---
title: "How to Auto-Sync Your CMDB with Zabbix Using Bash and MariaDB"
datePublished: Fri Jul 25 2025 08:24:56 GMT+0000 (Coordinated Universal Time)
cuid: cmdik2ubs001h02kzcu7d8qjr
slug: how-to-auto-sync-your-cmdb-with-zabbix-using-bash-and-mariadb
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1750848614407/c85c6274-ecca-4e0f-a109-b0f8b6d78b7b.png
tags: databases, devops, zabbix

---

Integrate your asset inventory with Zabbix seamlessly using a custom CMDB and automation. This guide walks you through creating a dynamic, real-time host inventory system using MariaDB, shell scripting, and the Zabbix API.

By the end of this post, you'll have a fully functioning setup that synchronizes your infrastructure database with Zabbix monitoring, ensuring complete visibility and consistency.

---

## 🧰 Prerequisites

* Linux server (RHEL/CentOS/Amazon Linux/Rocky recommended)
    
* Zabbix 7.0 LTS or newer
    
* MariaDB
    
* Root or sudo access
    
* Basic knowledge of Bash scripting, Zabbix API, SQL
    

---

## 🔧 Step 1: Zabbix Setup

### 🧱 Install Zabbix 7.0

```bash
# Add the Zabbix repo
wget https://repo.zabbix.com/zabbix/7.0/rhel/9/x86_64/zabbix-release-7.0-1.el9.noarch.rpm
rpm -ivh zabbix-release-7.0-1.el9.noarch.rpm
dnf clean all

# Install packages
sudo dnf install -y zabbix-server-mysql zabbix-web-mysql zabbix-nginx-conf \
  zabbix-sql-scripts zabbix-agent mariadb-server
```

### 🔐 Configure MariaDB for Zabbix

```bash
yum install mariadb-server
systemctl enable --now mariadb
mysql_secure_installation
```

Create the Zabbix DB:

```sql
CREATE DATABASE zabbix CHARACTER SET utf8mb4 COLLATE utf8mb4_bin;
CREATE USER zabbix@localhost IDENTIFIED BY 'zabbix_pass';
GRANT ALL PRIVILEGES ON zabbix.* TO zabbix@localhost;
FLUSH PRIVILEGES;
```

### 📥 Import Zabbix Schema

```bash
zcat /usr/share/zabbix-sql-scripts/mysql/server.sql.gz | mysql -uzabbix -p zabbix
```

### ⚙️ Start Zabbix Components

```bash
# Set DB password in /etc/zabbix/zabbix_server.conf
vim /etc/zabbix/zabbix_server.conf  # Set DBPassword=zabbix_pass

# Start services
systemctl enable --now zabbix-server zabbix-agent nginx php-fpm
```

Visit Zabbix UI: `http://<your-server-ip>/zabbix`

---

## 🗃️ Step 2: Setup CMDB in MariaDB

### 🛠️ Create the Database and Table

```sql
CREATE DATABASE service_now;
USE service_now;

CREATE TABLE cmdb_ci (
  sys_id VARCHAR(64) PRIMARY KEY,
  name VARCHAR(128),
  visible_name VARCHAR(128),
  ip_address VARCHAR(45),
  host_group VARCHAR(128),
  interface_type VARCHAR(16),
  proxy VARCHAR(64),
  env VARCHAR(64),
  its VARCHAR(64),
  os VARCHAR(128),
  sys_created_on DATETIME,
  sys_updated_on DATETIME
);
```

### 🧪 Insert Sample Data

```sql
INSERT INTO cmdb_ci (sys_id, name, visible_name, ip_address, host_group, interface_type, proxy, env, dept, os, sys_created_on, sys_updated_on)
VALUES
('a001', 'APP-SRV-001', 'App Server 1', '10.10.1.101', 'Application Servers', 'agent', 'proxy-eu', 'prod', 'Dept001', 'Windows Server 2019', NOW(), NOW()),
('a002', 'DB-SRV-001', 'DB Server 1', '10.10.3.101', 'Database Servers', 'snmp', 'proxy-us', 'uat', 'Dept002', 'RHEL 9', NOW(), NOW());
```

---

## 🧾 Step 3: Create the Zabbix Sync Script

### 🔗 Required Packages

```bash
sudo dnf install -y jq curl mariadb
```

### 🧩Template ID Mapping

In the shell script, templates are assigned based on OS values. Make sure these template IDs exist in your Zabbix system:

* **Windows hosts**: Template ID `10081` (e.g., "Windows by Zabbix agent")
    
* **Linux/Unix hosts**: Template ID `10001` (e.g., "Linux by Zabbix agent")
    

You can retrieve template IDs via API or from the Zabbix UI under Configuration → Templates.

### 📄 Script File `sync_db_zabbix.sh`

Create a shell script to do the following:

* Fetch all rows from `cmdb_ci`
    
* For each entry:
    
    * Determine group, proxy, templates
        
    * Add or update the host in Zabbix
        
    * Add macros, tags, and interfaces
        
* Optional: delete stale Zabbix hosts not in CMDB
    

```bash
#!/bin/bash

ZABBIX_URL="http://<zabbix_host>/api_jsonrpc.php"
ZABBIX_TOKEN="<your_zabbix_token>"
DB_NAME="service_now"
DB_USER="root"
DB_PASS="<your_db_password>"
DB_HOST="localhost"

# All logic to: get_host_id, get_or_create_group_id, get_proxy_id
# Loop through SQL results, parse, push to Zabbix
```

You can [find the complete working script here](https://github.com/ganesh4400/zabbix-cmdb-sync)

## 🤖 **Step 4: Automate with Cron**

Run the sync script daily:

```bash
chmod +x /root/zabbix-sync/sync_db_zabbix.sh
crontab -e
0 2 * * * /root/zabbix-sync/sync_db_zabbix.sh >> /var/log/zabbix_sync.log 2>&1
```

---

## ✅ Summary

In this guide, we:

* Installed and configured Zabbix and MariaDB
    
* Created a `service_now` database with a CMDB-like table
    
* Built a Bash script that reads from the DB and syncs with Zabbix
    
* Created dynamic host groups, proxies, templates, and tags
    

This solution helps eliminate manual host onboarding, ensuring your monitoring is always in sync with your asset inventory.

---

## 🧩 Future Enhancements

* Integrate directly with ServiceNow API
    
* Sync inventory fields like serial number, location, etc.
    
* Add robust logging with retry mechanisms
    
* Build CI/CD jobs using GitLab or Jenkins
    

---

*💬 Have feedback or enhancements? Share your comments or fork the repo and contribute!*

---

### 🪪 About the Author

*Written by* ***Ganesh Shinde***\*, a DevOps engineer passionate about Zabbix, automation, and systems monitoring. Follow for more infrastructure automation tips.\*

---

### 🔖 Tags

`zabbix` `cmdb` `devops` `bash` `mariadb` `monitoring` `automation`