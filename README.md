# 🔗 ftnt-automation-stitches

A comprehensive automation project for generating FortiGate CLI output and configuring devices remotely via API or Ansible. This repository provides modular configuration templates for FortiGate automation stitches with automated file combination workflows.

## 📋 Project Overview

A collection of CLI templates to create various parts of automation script routines. The project includes notification profiles (actions), event triggers, and automation stitches, all automatically combined through GitHub Actions workflows.

### 🏗️ Project Structure

```
├── actions/           # Notification profiles and automation actions
│   ├── ALL_ACTIONS.conf         # Auto-generated combined actions file
│   ├── formated-notification.conf
│   ├── to-slack.conf
│   └── to-teams.conf
├── triggers/          # Event-based automation triggers  
│   ├── ALL_TRIGGERS.conf        # Auto-generated combined triggers file
│   ├── admin-login.conf
│   ├── bgp-neighbor-state-changed.conf
│   ├── object-attribute-configured.conf
│   ├── routing-information-warning.conf
│   └── vpn-logon.conf
├── stitches/          # Automation workflows linking triggers to actions
│   ├── ALL_STITCHES.conf        # Auto-generated combined stitches file
│   └── vpn-connection-info.conf
├── .github/workflows/ # Automated file combination workflows
└── AUTOMATION-STITCHES.conf     # Master combined configuration file
```

## 🤖 Automated Workflows

The project includes GitHub Actions that automatically combine configuration files:

### Individual Component Workflows
- **`combine-actions-configs.yml`** - Combines all action files into [`actions/ALL_ACTIONS.conf`](actions/ALL_ACTIONS.conf)
- **`combine-triggers-configs.yml`** - Combines all trigger files into [`triggers/ALL_TRIGGERS.conf`](triggers/ALL_TRIGGERS.conf)  
- **`combine-stitches-configs.yml`** - Combines all stitch files into [`stitches/ALL_STITCHES.conf`](stitches/ALL_STITCHES.conf)

### Master Combination Workflow
- **`combine-all-configs.yml`** - Creates the master [`AUTOMATION-STITCHES.conf`](AUTOMATION-STITCHES.conf) file by combining all three component files

### 🔄 Workflow Triggers
- **Automatic**: Triggers when files are modified in respective directories
- **Cascading**: Master workflow runs when any component workflow completes
- **Manual**: All workflows support manual triggering via `workflow_dispatch`

## 📂 Configuration Files

### 📢 Actions (Notification Profiles)
Current implementations:
- ✅ **Microsoft Teams** - Formatted log notifications with webhook integration & Simple result forwarding
- ✅ **Slack** - Simple notification forwarding

### ⚡ Triggers (Event Detection)
Current implementations:
- ✅ **Admin Login** - Tracks administrator authentication events
- ✅ **BGP Neighbor State Changed** - Monitors BGP routing changes
- ✅ **Object Attribute Configured** - Detects configuration changes
- ✅ **Routing Information Warning** - Tracks routing protocol issues
- ✅ **VPN Logon** - Monitors VPN connection events

### 🔗 Stitches (Automation Workflows)
Current implementations:
- ✅ **VPN Connection Info** - Links VPN logon trigger to Teams notification

## 🎯 Automation Stitches Roadmap

### 📢 Notification Profiles

- [x] **Teams** integration (formatted and basic)
- [x] **Slack** integration  
- [ ] **Discord** integration
- [ ] **E-Mail** notifications
- [ ] **SNMP** trap forwarding
- [ ] **Syslog** forwarding

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
- [ ] Amount of HW accelerated sessions are low
- [ ] Hardware reboot detection

#### 👨‍💼 Administration
- [x] **Config changes** (object-attribute-configured)
- [x] **Login tracker** (admin-login)
- [ ] Password change tracker
- [ ] Backup configuration to SFTP
- [ ] Certificate expiration warnings

#### 🔄 High Availability (HA)
- [ ] Cluster state changed
- [ ] Member dead
- [ ] Cluster not in sync
  - [ ] Cluster not in sync, recalculate
  - [ ] Cluster not in sync, export hashes to notification profile

#### 🌐 Network Interfaces
- [ ] Any Interface goes down
- [ ] Any Interface goes up
- [x] **VPN Tunnels** up/down (vpn-logon)

#### 🛡️ FortiGuard Services
- [ ] FortiGuard unreachable
- [ ] Download updates
- [ ] Antivirus definition updates
- [ ] IPS signature updates

#### 🌐 Routing & Network
- [x] **BGP neighbor changes** (bgp-neighbor-state-changed)
- [x] **Routing warnings** (routing-information-warning)
- [ ] OSPF neighbor changes
- [ ] Static route failures
- [ ] Link state changes

---

## 🚀 Getting Started

### Adding New Configurations

1. **Create individual config files** in the appropriate directory:
   - `actions/` for notification profiles
   - `triggers/` for event triggers  
   - `stitches/` for automation workflows

2. **Follow the FortiGate CLI format**:
   ```bash
   config system automation-action
       edit "Action Name"
           set description 'Description here'
           # ... configuration ...
       next
   end
   ```

3. **Commit changes** - GitHub Actions will automatically:
   - Combine files in the modified directory
   - Update the master [`AUTOMATION-STITCHES.conf`](AUTOMATION-STITCHES.conf) file
   - Skip auto-generated header comments

### Using the Generated Configurations

The master [`AUTOMATION-STITCHES.conf`](AUTOMATION-STITCHES.conf) file contains the complete configuration ready for:
- **CLI Import**: Copy/paste directly into FortiGate CLI
- **API Deployment**: Use with FortiGate REST API
- **Ansible Playbooks**: Import via `fortios_configuration_fact` module

### Variable Usage in Actions

Actions support FortiGate variables for dynamic content:

#### Log Variables
- `%%log%%` - Complete log entry
- `%%log.user%%` - Username from log
- `%%log.date%%` - Log date
- `%%log.time%%` - Log timestamp
- `%%log.msg%%` - Log message
- `%%log.subtype%%` - Log subtype

#### Results Variables  
- `%%results%%` - Previous action results
- `%%results.property%%` - Specific result property
- `%%results[action_name].value%%` - Result from named action

## 📝 External Documentation

- [FortiGate Administration Guide - Variables in Actions](https://docs.fortinet.com/document/fortigate/7.6.3/administration-guide/427797/variables-in-actions)
- [FortiGate Automation Stitches Overview](https://docs.fortinet.com/document/fortigate/7.6.3/administration-guide/139441/automation-stitches)

## 📄 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.
