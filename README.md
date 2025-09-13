# Red Team Automated Scoring Disruption Playbook

## Overview
This Caldera playbook is designed to automate red team operations that break blue team score checks in red vs blue environments. The playbook systematically targets critical services and infrastructure to disrupt monitoring and scoring systems.

## Attack Progression

### Level 1: Service Disruption (Impact - T1489)
**Objective**: Stop critical services to break blue team scoring checks
- **NFS Service**: Stop network file sharing
- **DNS Service**: Stop bind9 DNS resolution
- **WikiJS**: Stop documentation service (Docker container)
- **FTP Service**: Stop file transfer protocol service
- **SSH Service**: Stop secure shell access
- **MySQL Database**: Stop database service
- **VNC Server**: Stop remote desktop service
- **Silkroad**: Stop custom web application
- **Gitea**: Stop git repository service
- **Mail Server**: Stop email services (Docker container)
- **Roundcube**: Stop webmail interface (Docker container)
- **SSHD (rowboat)**: Stop SSH daemon on specific host

### Level 2: Service Evasion (Defense Evasion - T1562.001)
**Objective**: Change service configurations to evade detection and break scoring
- **SSH Port Change**: Move SSH from port 22 to 2222
- **DNS Port Change**: Move DNS from port 53 to 5300
- **FTP Port Change**: Move FTP from port 21 to 2121
- **WikiJS Port Change**: Redeploy container on port 8080
- **VNC Port Change**: Move VNC to port 5999
- **SSHD Port Change**: Move SSH daemon to port 2222
- **Mail Server Ports**: Change SMTP (25→2525), IMAP (143→1143), submission (587→1587)
- **MySQL Port Change**: Move MySQL from port 3306 to 3309
- **Silkroad Port Change**: Move from port 3000 to 69
- **Gitea Port Change**: Move HTTP service to port 8085
- **Database Permission Revocation**: Remove SELECT permissions from sqluser
- **Roundcube Port Change**: Move webmail from port 8080 to 8181

### Level 3: Account and Data Manipulation
**Objective**: Manipulate access controls and data integrity
- **SSH Access Denial** (T1098): Add dreadpirate user to SSH DenyUsers list
- **Database Manipulation** (T1565.001): Change product names in database
- **DNS Zone Replacement** (T1560.001): Replace DNS zone with minimal configuration, hide backup

### Level 4: Network and System Disruption
**Objective**: Block network access and destroy web content
- **SSH Firewall Block** (T1562.004): Block inbound/outbound SSH traffic on ports 22 and 2222
- **DNS IP Blackholing** (T1562.006): Block scorecheck IP (10.0.0.80) in DNS
- **Web Content Destruction** (T1565.001): Replace Silkroad webroot with empty directory

## Usage
1. Deploy this playbook in your Caldera instance
2. Target systems with appropriate Linux platform access
3. Execute operations in level order for maximum scoring disruption
4. Monitor blue team response and scoring system impact

## MITRE ATT&CK Techniques Used
- **T1489**: Service Stop
- **T1562.001**: Impair Defenses: Disable or Modify Tools
- **T1562.004**: Impair Defenses: Disable or Modify System Firewall
- **T1562.006**: Impair Defenses: Indicator Blocking
- **T1098**: Account Manipulation
- **T1565.001**: Data Manipulation: Stored Data Manipulation

## Target Services
- Network Services: SSH, FTP, DNS, NFS
- Web Services: WikiJS, Silkroad, Gitea, Roundcube
- Database Services: MySQL
- Mail Services: Mailserver stack
- Remote Access: VNC, SSH

**Warning**: This playbook is designed for authorized red team exercises only. Ensure proper authorization before deployment.