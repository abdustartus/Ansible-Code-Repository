# Infrastructure Config & Automation (Ansible)

Once AWS hardware is up (via Terraform), this repo handles the OS config. It turns raw Ubuntu servers into a hardened **Jenkins Master** and **Docker-ready app host** for the deployment pipeline.

## What It Does
**Jenkins Master Setup**  
- Installs OpenJDK 11 (Jenkins requirement).  
- Configures Jenkins LTS repo and installs.  
- Starts service + enables on boot.  

**Docker App Host**  
- Installs Docker engine + dependencies.  
- Adds ubuntu user to docker group (key for Jenkins SSH agents—no sudo hassles).  
- Preps for Node.js container deploys.

## File Structure
- hosts.yaml: AWS Private IPs + SSH details  
- dockerplaybook.yml: Main orchestration playbook  
- main.yml: Core install tasks  
- upgrad-key.pem: SSH private key (gitignored)  

## Run It
1. **Check connectivity**: ansible all -m ping -i hosts.yaml  
2. **Execute**: ansible-playbook -i hosts.yaml dockerplaybook.yml  

## Done
After a successful run, the Jenkins Master will be accessible on port 8080, and the App Host will be ready to pull and run images from Amazon ECR.

