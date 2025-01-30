# LSSA - Lynis Server Security Auditing

LSSA (Lynis Server Security Auditing) is a Docker-based solution that automates security auditing on multiple remote servers using **Lynis** and **Ansible**. It performs system hardening checks and generates detailed HTML security reports for each server.

## Features
- Automates security audits on multiple remote servers.
- Uses **Lynis** for in-depth system security checks.
- Generates reports in a **readable HTML format**.
- Saves all reports inside the container and syncs them to the host machine.
- **Uses Ansible** for seamless automation.
- **Docker-based setup**, making deployment easy.
- Runs on **host networking mode** for better connectivity.

## How It Works
1. A Docker container (`lssa_atul`) runs **Ansible** inside it.
2. The container connects to multiple remote servers over SSH.
3. Ansible runs **Lynis** on each remote server.
4. Lynis audits the security of the remote servers and generates reports.
5. The generated reports are saved in the container under `/atul/lynis_ansible/reports`.
6. These reports are **bind-mounted** to the host machine for easy access.

## Installation
### 1. Clone the Repository
```bash
 git clone https://github.com/ATUL9372/LSSA-Docker.git
 cd LSSA-Docker
```

### 2. Update Inventory (Hosts File)
Modify `hosts` file to add your remote server IPs and authentication details.

```ini
[test]
# Enter all remote server ip's
192.16X.XX.XX

[test:vars]

ansible_connection=ssh
ansible_ssh_user=USERNAME
ansible_become_password=PASSWORD
ansible_ssh_pass=PASSWORD
#ansible_ssh_common_args='-o IdentitiesOnly=yes'
ansible_ssh_common_args='-o StrictHostKeyChecking=no'
```

### 3. Run LSSA Using Docker Compose
```bash
docker-compose up -d
```

This will:
- Start a container with **Ansible** inside it.
- Run the **Lynis audit** on remote machines.
- Store reports in `lynis_reports/` on your host machine.

### 4. Access the Reports with sudo permission
Once the audit is completed, reports will be available in `lynis_reports/`.
```bash
ls -l lynis_reports/
```

## Stopping & Removing the Container
```bash
docker-compose down
```
