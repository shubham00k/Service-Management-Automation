# Service Management Automation on EC2 using Ansible

📌 **Automates starting, stopping, and enabling services (httpd, nginx, docker) on AWS EC2 instances using Ansible.**  

## Overview
This project uses **Ansible** to automate the management of system services on remote AWS EC2 instances.  
You can use it to:  
✅ Install services like **Apache (httpd), Nginx, or Docker**  
✅ Start/stop services automatically  
✅ Enable services to run at boot  

## Prerequisites
### 1. Install Ansible
If you don’t have Ansible installed, install it using:  
**For Ubuntu/Debian:**  
```bash
sudo apt update && sudo apt install ansible -y
```
**For CentOS/RHEL:**  
```bash
sudo yum install ansible -y
```

### 2. Configure AWS EC2 Instance
- Launch an **EC2 instance** in AWS.  
- Ensure it has **SSH access** from your local machine.  
- Copy your **EC2 instance’s private key file** (`.pem`) to your local system.  

### 3. Set Up Ansible Inventory File
Edit the `inventory` file and replace `your-ec2-ip` with the **actual EC2 IP**:
```ini
[webservers]
your-ec2-ip ansible_ssh_user=ec2-user ansible_private_key_file=~/.ssh/your-key.pem
```

## Project Structure
```
Service-Management-Automation/
│── README.md         # Documentation  
│── ansible.cfg       # Ansible configuration file  
│── inventory         # List of remote servers  
│── playbook.yml      # Ansible playbook  
```

## Usage
### Step 1: Test Connection
Run the following command to verify that Ansible can connect to the EC2 instance:  
```bash
ansible all -m ping
```

If the connection is successful, you should see:  
```
your-ec2-ip | SUCCESS => {
    "changed": false,
    "ping": "pong"
}
```

### Step 2: Run the Ansible Playbook
```bash
ansible-playbook playbook.yml
```

### Expected Output
After running the playbook, the **httpd service** will be:  
✅ **Installed** if not already present  
✅ **Started** if it’s not running  
✅ **Enabled** to start automatically on boot  

## Troubleshooting
1. **Permission Denied (SSH Key Issue)**  
   ```
   Permission denied (publickey,gssapi-keyex,gssapi-with-mic).
   ```
   ✅ Ensure your `.pem` key has correct permissions:  
   ```bash
   chmod 400 your-key.pem
   ```

2. **Playbook Fails with ‘sudo password required’**  
   ✅ Add `become: true` to **all tasks** in `playbook.yml`.  

## Next Steps
- Extend this playbook to manage **multiple services** (nginx, docker, mysql).  
- Create a **role-based structure** for better organization.  
- Integrate this playbook with **CI/CD pipelines** for automated deployments.  
