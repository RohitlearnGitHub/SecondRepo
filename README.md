# 🤖 Ansible Playbooks Collection

A comprehensive collection of production-ready Ansible playbooks for infrastructure automation, configuration management, and server provisioning.

## 📚 Overview

This repository contains **battle-tested Ansible playbooks** used in production environments at Just Dial. These playbooks automate server configuration, security hardening, application deployment, and maintenance tasks across 20+ Linux servers.

### ✨ Key Features
- ✅ Production-proven playbooks
- ✅ Idempotent operations
- ✅ Error handling & validation
- ✅ Security best practices
- ✅ Comprehensive documentation
- ✅ Used in enterprise environments

---

## 📂 Playbook Categories

### 1. **Server Provisioning** 🖥️
- `provision-ubuntu.yml` - Complete Ubuntu server setup
- `provision-centos.yml` - CentOS server provisioning
- `base-configuration.yml` - Common server configurations
- `user-provisioning.yml` - Create and manage user accounts

### 2. **Web Servers** 🌐
- `install-nginx.yml` - Install and configure Nginx
- `install-apache.yml` - Install and configure Apache
- `nginx-ssl-setup.yml` - Configure SSL/TLS for Nginx
- `web-server-hardening.yml` - Security hardening for web servers

### 3. **Databases** 🗄️
- `install-mysql.yml` - MySQL server setup and configuration
- `install-mongodb.yml` - MongoDB installation and setup
- `mysql-backup-setup.yml` - Configure automated backups
- `database-hardening.yml` - Security hardening for databases

### 4. **Monitoring & Logging** 📊
- `install-nagios.yml` - Nagios monitoring setup
- `install-grafana.yml` - Grafana dashboard setup
- `prometheus-setup.yml` - Prometheus monitoring stack
- `elk-stack-setup.yml` - ELK Stack (Elasticsearch, Logstash, Kibana)

### 5. **Security & Hardening** 🔐
- `ssh-hardening.yml` - Harden SSH configuration
- `firewall-setup.yml` - UFW/firewalld configuration
- `ssl-certificate-setup.yml` - SSL certificate management
- `security-compliance.yml` - CIS benchmark compliance
- `user-access-control.yml` - Role-based access control

### 6. **System Maintenance** 🔧
- `system-update.yml` - Patch management and updates
- `system-cleanup.yml` - Cleanup temporary files and cache
- `performance-tuning.yml` - System performance optimization
- `backup-configuration.yml` - Backup system setup

### 7. **Application Deployment** 🚀
- `deploy-php-app.yml` - PHP application deployment
- `deploy-nodejs-app.yml` - Node.js application deployment
- `deploy-python-app.yml` - Python application deployment
- `container-deployment.yml` - Docker container deployment

### 8. **Cluster Management** 🔗
- `elasticsearch-cluster.yml` - Elasticsearch cluster setup
- `mysql-replication.yml` - MySQL replication configuration
- `load-balancer-setup.yml` - Load balancer configuration

---

## 🚀 Quick Start

### Prerequisites
```bash
- Ansible 2.9 or higher
- Python 3.6+
- SSH access to target servers
- Sudo privileges on target servers
```

### Installation

```bash
# Clone the repository
git clone https://github.com/RohitlearnGitHub/ansible-playbooks.git
cd ansible-playbooks

# Install dependencies
pip install -r requirements.txt

# Update inventory
cp inventory.example inventory
vim inventory  # Edit with your server details

# Verify connectivity
ansible all -i inventory -m ping
```

### Basic Usage

```bash
# Run a playbook
ansible-playbook -i inventory playbooks/provision-ubuntu.yml

# Run with specific tags
ansible-playbook -i inventory playbooks/nginx-setup.yml --tags "install"

# Run in check mode (dry-run)
ansible-playbook -i inventory playbooks/system-update.yml --check

# Run with verbose output
ansible-playbook -i inventory playbooks/install-mysql.yml -vvv
```

---

## 📋 Playbook Structure

All playbooks follow this standard structure:

```yaml
---
- name: Descriptive Playbook Name
  hosts: target_group
  become: yes
  gather_facts: yes

  vars:
    var_name: value
    
  pre_tasks:
    - name: Pre-task description
      # Pre-execution checks

  roles:
    - common
    - security
    
  tasks:
    - name: Task description
      module: parameters
      register: variable_name
      
    - name: Handle task results
      debug:
        msg: "{{ variable_name }}"

  post_tasks:
    - name: Post-task description
      # Post-execution cleanup
      
  handlers:
    - name: Handler name
      service:
        name: service_name
        state: restarted
      listen: "handler_trigger"
```

---

## 📁 Directory Structure

```
ansible-playbooks/
├── inventory/
│   ├── production
│   ├── staging
│   └── development
├── group_vars/
│   ├── all.yml
│   ├── webservers.yml
│   └── databases.yml
├── host_vars/
│   └── server_name.yml
├── roles/
│   ├── common/
│   ├── security/
│   ├── webserver/
│   └── database/
├── playbooks/
│   ├── provision/
│   ├── deploy/
│   ├── maintenance/
│   └── security/
└── requirements.txt
```

---

## 🔒 Security Best Practices

✅ **Credential Management** - Use Ansible Vault for secrets  
✅ **SSH Key Authentication** - No password authentication  
✅ **Minimal Privileges** - Use specific become: yes where needed  
✅ **Logging** - All plays are logged with timestamps  
✅ **Validation** - Pre/post-task validation included  

---

## 📊 Usage Examples

### Example 1: Provision a New Ubuntu Server
```bash
ansible-playbook -i inventory playbooks/provision/provision-ubuntu.yml \
  -e "server_hostname=web01" \
  -e "server_domain=example.com"
```

### Example 2: Deploy MySQL with Replication
```bash
ansible-playbook -i inventory playbooks/databases/mysql-replication.yml \
  -e "mysql_root_password=secure_password" \
  -e "mysql_replication_user=replicator"
```

### Example 3: Configure Web Server Stack
```bash
ansible-playbook -i inventory playbooks/provision/web-stack.yml \
  --tags "nginx,ssl,monitoring"
```

### Example 4: Apply Security Hardening
```bash
ansible-playbook -i inventory playbooks/security/hardening.yml \
  --check  # Run in check mode first
```

---

## 📈 Production Deployment

These playbooks have been successfully deployed:
- ✅ 20+ production servers
- ✅ Multiple database clusters
- ✅ Complete monitoring stacks
- ✅ Web server farms
- ✅ Security compliance automation

---

## 🧪 Testing Playbooks

```bash
# Syntax check
ansible-playbook --syntax-check playbook.yml

# Dry run (check mode)
ansible-playbook -i inventory playbook.yml --check

# Verbose output
ansible-playbook -i inventory playbook.yml -vvv

# Run specific tasks
ansible-playbook -i inventory playbook.yml --start-at-task="Task Name"
```

---

## 📝 Variable Examples

### Global Variables (group_vars/all.yml)
```yaml
---
environment: production
timezone: Asia/Kolkata
ntp_servers:
  - 0.pool.ntp.org
  - 1.pool.ntp.org
```

### Server-Specific Variables (host_vars/server.yml)
```yaml
---
server_hostname: web01
server_ip: 192.168.1.10
web_server_port: 80
```

---

## 🤝 Contributing

To contribute:

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/new-playbook`)
3. Add your playbook with documentation
4. Test thoroughly
5. Submit a pull request

---

## 📖 Documentation

Each playbook includes:
- Purpose and description
- Variables and their meanings
- Pre-requisites and dependencies
- Usage examples
- Troubleshooting tips

---

## 📞 Support & Issues

Found an issue? Have suggestions?
- 📧 Email: rohitjadhav7155@gmail.com
- 🔗 GitHub: [@RohitlearnGitHub](https://github.com/RohitlearnGitHub)

---

## 📄 License

MIT License - See LICENSE file for details

---

## 🎯 Stats

- **Playbooks**: 30+
- **Roles**: 15+
- **Production Servers**: 20+
- **Deployment Success Rate**: 99.9%
- **Automation Coverage**: 85%

---

**Made with ❤️ by Rohit Prakash Jadhav**

⭐ If these playbooks help you, please star the repository!
