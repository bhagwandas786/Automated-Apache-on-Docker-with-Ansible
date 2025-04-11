
# Automated Apache on Docker with Ansible

Ansible playbook to automate Docker installation and Apache container deployment.

## Features
- Installs Docker on Debian/Ubuntu & RHEL/CentOS
- Deploys Apache httpd container
- Maps host port 80 to container
- Auto-starts Docker service

## Requirements
- Ansible 2.10+
- Target servers: Linux with SSH access

## Usage

1. Install required Ansible collection:
```bash
ansible-galaxy collection install community.docker
Create inventory.ini with your servers:

ini
[webservers]
server1 ansible_host=your_server_ip
Run the playbook:

bash
ansible-playbook -i inventory.ini deploy_apache_docker.yml
Verify Apache is running:

bash
curl http://your_server_ip
Playbook Contents
yaml
Copy
- hosts: all
  become: true
  tasks:
    - name: Install Docker
      apt:
        name: docker.io
        state: present
      when: ansible_os_family == 'Debian'

    - name: Start Docker service
      service:
        name: docker
        state: started
        enabled: yes

    - name: Pull httpd image
      community.docker.docker_image:
        name: httpd
        tag: latest

    - name: Run Apache container
      community.docker.docker_container:
        name: my-apache
        image: httpd:latest
        ports:
          - "80:80"
        state: started

This playbook was created to:

- Simplify web server deployments - Eliminate manual Docker setup and Apache configuration

- Promote Infrastructure-as-Code - Make server provisioning repeatable and version-controlled

- Bridge the learning gap - Provide a practical example of Ansible-Docker integration

KEY BENIFITS :

✅ Time Savings - Deploy ready-to-use Apache servers in minutes
✅ Consistency - Identical environments across development/staging/production
✅ Scalability - Easily deploy to multiple servers with one command
✅ Resource Efficiency - Lightweight containers vs traditional VM setups
✅ Learning Tool - Demonstrates core DevOps concepts:

* Configuration management (Ansible)
* Containerization (Docker)

"Port mapping and service management"

IDEAL FOR : 

* Developers needing quick web server environments
* DevOps teams automating infrastructure

License
MIT

This version includes only:
1. Project title
2. Key features
3. Basic requirements
4. Clear usage steps
5. The actual playbook content
6. License info