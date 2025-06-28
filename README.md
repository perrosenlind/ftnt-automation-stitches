# 🔗 ftnt-automation-stitches

A comprehensive automation project for generating FortiGate CLI output and configuring devices remotely via API or Ansible.

## 📋 Project Overview

Create a script that can generate CLI output or configure directly on the remote FortiGate via API or Ansible.

## 🎯 Automation Stitches Roadmap

### 📢 Notification Profiles

- [ ] **Teams** integration
- [ ] **Slack** integration  
- [ ] **Discord** integration
- [ ] **E-Mail** notifications

### ⚡ Events & Triggers

#### 🚨 Conserve Mode
- [ ] Conserve mode triggered, notify only
- [ ] Conserve mode triggered, reboot
- [ ] Conserve mode triggered, restart wad
- [ ] Conserve mode triggered, restart ips

#### 📊 Performance Monitoring
- [ ] CPU usage reaches X %
- [ ] Memory usage reaches X %
- [ ] Disk usage reaches X %
- [ ] Amount of sessions reaches X value
- [ ] Amount of new sessions reaches X value
- [ ] Amount of HW accelerated sessions are low (try to see if it's possible to do math in stitches)
- [ ] Hardware reboot

#### 👨‍💼 Administration
- [ ] Audit log with config changes
- [ ] Login tracker
- [ ] Password change tracker
- [ ] Backup configuration to SFTP

#### 🔄 High Availability (HA)
- [ ] Cluster state changed
- [ ] Member dead
- [ ] Cluster not in sync
  - [ ] Cluster not in sync, recalculate
  - [ ] Cluster not in sync, export hashes to notification profile

#### 🌐 Network Interfaces
- [ ] Any Interface goes down
- [ ] Any Interface goes up
- [ ] VPN Tunnels up/down

#### 🛡️ FortiGuard Services
- [ ] FortiGuard unreachable
- [ ] Download updates

---

## 🚀 Getting Started

*Implementation details and setup instructions coming soon...*

## 📝 Contributing

*Contribution guidelines coming soon...*
