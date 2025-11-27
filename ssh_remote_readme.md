# SSH Remote Server Setup

![SSH Logo](https://www.hostinger.com/tutorials/wp-content/uploads/sites/2/2017/07/asymmetric-encryption.webp)

## Project Goal
The goal of this project is to setup a basic remote Linux server and configure it to allow SSH connections using two different SSH key pairs.

---

## Steps Completed

1. **Setup VM as a Linux server**  
   - Ubuntu 24.04 LTS VM running on local environment.

2. **Created two SSH key pairs**  
   ```bash
   ssh-keygen -t rsa -b 4096 -f ~/.ssh/my-first-project
   ssh-keygen -t rsa -b 4096 -f ~/.ssh/my-second-key
   ```

3. **Added public keys to the VM**  
   ```bash
   mkdir -p ~/.ssh
   cat ~/my-first-project.pub >> ~/.ssh/authorized_keys
   cat ~/my-second-key.pub >> ~/.ssh/authorized_keys
   chmod 600 ~/.ssh/authorized_keys
   ```

4. **Configured SSH config for easy access**  
   ```text
   Host myvm
       HostName 192.168.94.128
       User sara
       IdentityFile ~/.ssh/my-first-project
       IdentityFile ~/.ssh/my-second-key
   ```

5. **Verified connection with both keys**  
   ```bash
   ssh -i ~/.ssh/my-first-project sara@192.168.94.128
   ssh -i ~/.ssh/my-second-key sara@192.168.94.128
   ssh myvm
   ```

6. **Optional:** Installed fail2ban to prevent brute-force attacks
   ```bash
   sudo apt update
   sudo apt install fail2ban
   sudo systemctl enable fail2ban
   sudo systemctl start fail2ban
   ```

---


