Requirements:
- OS Ubuntu 20.04
- Host must be reacheble over network over SSH
- User with SUDO rights
- Change ip address in this file "./hosts.txt".
  Several IP addresses can be entered here, then the installation will be carried out on several systems at the same time
- Change this parameter "ansible_user" in "./group_vars/DOCKER_SERVER"
  As value enter the username of remote system.
- Change this parameter "ansible_ssh_private_key_file" in folowing files "./group_vars/DOCKER_SERVER" & "./roles/install_docker_server/vars/main.yml".
  As value enter the path to your own SSH private key here. (Example /home/user/.ssh/id_rsa)
- In task 3. "autorized_key" change parameter "key" in folowing file "./playbook_create_docker_user.yml".
  As value enter the path to your own SSH public key here. (Example /home/user/.ssh/id_rsa.pub)

Steps:
1. Copy SSH public key on remote host without docker user.
Enter the correct IP address of the target system here.

--
ssh-copy-id user@192.168.x.x
--

1.1 Verify whether you can log in via SSH without entering the password .
Enter the correct IP address of the target system here.

--
ssh user@192.168.x.x
--

2. Create Docker user with SUDO rights, copy SSH key.
User "docker" with password "docker" is created here.
!!! the command requires the password of the "user" to be entered. !!!

--
ansible-playbook playbook_create_docker_user.yml -K
--

3. Install Docker and Docker-Compose using a role.
Execution is started with the user "docker".
The password "docker" must be entered here for SUDO authorization.

-- 
ansible-playbook playbook_install_docker_role.yml -K
--
