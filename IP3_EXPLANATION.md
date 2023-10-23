IP 3 EXPLANATION
Setup aplication server
I Created 3 roles as illustrated in Playbook.yml file
    1. vm-config - This was to install dependancies
    2. docker-install - This had several roles in it, to Docker Add GPG apt Key, Install Docker,Docker Compose Installation, Docker Restart just to mention afew. To see all the roles you can check the main.yml here denisIP2/docker_install/tasks/main.yml
    3. Clone & run docker

    
# The purpose of this IP is to set up an automated Ansible configuration playbook that automates the following configurations on a Vagrant provisioned server. 
# a. Ansible Instrumentation
# b. Ansible and (Terraform - OPTIONAL)  instrumentation

1. # VAGRANT FILE
    To generate tis file on the root folder, i used Vagra Init command. The vagrant file has the following
    Configuration Version: This Vagrantfile specifies that it uses configuration version 2 (Vagrant.configure("2")). This version is commonly used and provides a structured way to define the virtual machine's settings.

    i. Box Selection: It specifies the base box to use for the virtual machine. In this case, it's using the "geerlingguy/ubuntu2004" box, which is 
       an  Ubuntu 20.04 image. The box serves as the base operating system for the virtual machine.
    ii. Port Forwarding: It sets up port forwarding from the host machine to the guest virtual machine. Port 3000 and 5000 on the host machine are      
        forwarded to port 3000 and 5000 on the guest machine, respectively. This allows services running on the guest machine to be accessible from the host.
    iii. Private Network (Optional): There's a commented-out section for creating a private network with a specific IP address (e.g., "192.168.33.10").  
         This would allow the host to communicate with the guest machine on a private network.
    iv. Public Network (Optional): There's also a commented-out section for creating a public network, which would make the virtual machine appear as 
        another physical device on your network. This is often used when you want to expose the VM to other devices on your network.
    v. Synced Folder (Disabled): It defines a synced folder between the host and guest machine. The first argument specifies the host path, the second 
       argument specifies the guest path, and the third argument (in this case, "disabled: true") disables the synced folder. The dot (".") represents the current directory, and the "/vagrant" path on the guest machine is where the host's files would be available. However, it's disabled in this configuration.
    vi. Provider-Specific Configuration (VirtualBox): It includes some provider-specific configuration for VirtualBox, a common virtualization provider 
        for Vagrant. It customizes the VirtualBox VM settings, such as disconnecting a virtual UART device and setting the VM's memory to 2048 MB.
    Vii. Provisioning with Ansible (Optional): This configuration specifies provisioning using Ansible, a configuration management tool. It tells Vagrant 
        to run an Ansible playbook named "playbook.yml" and be verbose during the provisioning process.

    In summary, the Vagrantfile sets up a virtual machine based on the "geerlingguy/ubuntu2004" box, configures port forwarding, optionally sets 
    up private and public networks, disables a synced folder, configures specific VirtualBox settings, and optionally provisions the VM using Ansible by running a playbook.

2. # PLAYBOOK
    This is an Ansible playbook written in YAML format. It is used to set up Yolo on an Ubuntu Server 22.04 machine.

    The main components of the Ansible playbook.yml are explain below:-
    name: A descriptive name for the playbook. In this case, it's "Setup Yolo on Ubuntu Server 22.04," providing a high-level description of what the playbook does.

    a. hosts: Specifies the target hosts on which the tasks in this playbook will be executed. "all" means that the tasks will be executed on all hosts 
       defined in the inventory file.
    b. become: This parameter is set to "true," which means that the tasks within this playbook will run with elevated privileges. In this case, Ansible 
       will use sudo to execute tasks as the root user.
    c. remote_user: Specifies the user that Ansible will use to connect to the target hosts. It's set to "root" in this playbook, indicating that Ansible 
       will connect to the target hosts using the root user.
    d. gather_facts: When set to "true," this option enables Ansible to collect facts about the target hosts, such as system information and available 
       resources.
    e. become_method: Specifies the method Ansible should use to become an elevated user (usually "sudo" for privilege escalation).
    g. become_user: Specifies the user to become when using privilege escalation. It's set to "root" in this playbook, so Ansible will become the root 
       user when executing tasks with elevated privileges.
    f. become_flags: These flags are additional options for privilege escalation. In this case, "-H -S -n" are specified. These flags typically control 
       how authentication and environment variables are handled when becoming the elevated user.
    g. vars: This section allows you to define variables that can be used within the playbook. In this playbook, it sets the ansible_python_interpreter 
       variable to "/usr/bin/python3." This variable specifies the path to the Python interpreter that Ansible should use when executing tasks on the target hosts.
    h.  roles: This is a list of Ansible roles that will be executed as part of the playbook. Roles are a way to organize and reuse Ansible tasks and 
       configurations. The playbook includes the following roles:
            i. vm-config: Presumably, this role is responsible for configuring the virtual machine.
            ii. docker_install: This role is likely responsible for installing Docker on the system.
            iii. clone_rundcoker: This role may involve cloning a Docker-related repository and running Docker containers.

3. # ROLES
As you can see in the playbook.yml, I created 3 roles as explaied below
 1. # vm-config 
    The purpose of this "vm-config" role is to prepare the virtual machine by ensuring that it has the necessary software packages and dependencies installed. This is a common initial step when setting up a system for development or specific tasks. The role ensures that the system is up-to-date and equipped with essential tools and libraries, which can then be used by subsequent Ansible roles or tasks to configure the machine for its intended purpose, such as running applications or services.
    
2. # docker-install
    It contains tasks that are responsible for installing and configuring Docker on the target system.
    The purpose of this "docker_install" role is to automate the installation and initial configuration of Docker on the target system, making it ready for containerization and container management. It also sets up a non-root user for Docker access, installs Python modules for Docker management, and configures Docker Compose for multi-container applications.

3. # clone_rundcoker
    This contains tasks that are responsible for cloning a repository from GitHub and running a Docker Compose setup in the cloned directory.
    The purpose of this "clone_rundcoker" role is to automate the process of setting up a specific application or service by cloning its source code from a GitHub repository and running it with Docker Compose. This role streamlines the deployment of the application, making it easier to manage and ensuring that the application is running in a containerized environment. It simplifies tasks such as code retrieval, directory setup, and container orchestration.


4.  # LAUNCHING OF THE APP
 To launch the app, I used commands such as
  1. vagrant up
  2. vagrant ssh