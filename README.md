# ⚙️ Configuration Management with Ansible

Welcome to the **Configuration Management** project! This repo automates the setup of a web server using **Ansible**, provisioning an **NGINX** server, uploading and extracting a website tarball, managing SSH access, and ensuring reproducible deployment across environments.

---

## 📁 Project Structure

```
Configuration-Management/
├── inventory.ini                    # Inventory file with target hosts
├── setup.yml                        # Master playbook
├── roles/
│   ├── app/
│   │   ├── files/
│   │   │   └── webserver.tar        # Your website files
│   │   ├── tasks/
│   │   │   └── main.yml             # Handles upload & extraction of web content
│   ├── base/
│   │   └── main.yml                 # Placeholder (currently empty)
│   ├── nginx/
│   │   ├── handlers/
│   │   │   └── main.yml             # Handler to reload NGINX
│   │   ├── tasks/
│   │   │   └── main.yml             # Install & configure NGINX
│   │   └── templates/
│   │       └── default.conf.j2      # NGINX configuration template
│   ├── ssh/
│   │   ├── files/
│   │   │   └── id_rsa.pub           # Public key to deploy to remote servers
│   │   ├── tasks/
│   │   │   └── main.yml             # Adds SSH key & user setup
```

---

## 🚀 Features

- ✅ NGINX installation & configuration via Jinja2 template  
- 📦 Website tarball deployment and extraction  
- 🔐 Secure SSH key-based access setup  
- 🔄 Auto-reload NGINX using Ansible handler  
- 🧩 Modular role-based Ansible architecture  

---

## 📜 How to Use

### 1. 🔧 Prerequisites

- Ansible installed on the control node
- One or more Linux-based target servers (e.g., EC2 instance)
- SSH access set up to target machines

### 2. 🧾 Inventory

Edit the `inventory.ini` file to include your server's IP:

```ini
[web]
<ip> ansible_user=ec2-user ansible_ssh_private_key_file=~/.ssh/id_rsa
```

### 3. 🚦 Run Playbook

```bash
ansible-playbook -i inventory.ini setup.yml
```

This command:

- Installs NGINX
- Sets up the web directory
- Uploads and extracts `webserver.tar`
- Deploys the NGINX config
- Adds SSH key for a `deploy` user

---

## 💡 Troubleshooting Tips

- ❗ **Not extracting tarball?**  
  Make sure `webserver.tar` is a valid tar file. Test manually with:
  ```bash
  tar -tvf webserver.tar
  ```

- ♻️ **Changes not visible?**  
  NGINX may need to be reloaded. Ensure your handler is triggered properly or run:
  ```bash
  sudo systemctl reload nginx
  ```

---

## 👤 Author

Made with ❤️ by **[Sachin Dayal](https://github.com/Sachin-960)**  
🛠️ Focused on DevOps | Cloud | Automation | Cybersecurity

---

This is a part of the [Roadmap.sh](https://roadmap.sh/projects/configuration-management) Devops Projects.
