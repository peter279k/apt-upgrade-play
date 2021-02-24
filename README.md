# apt-upgrade-play

# Prerequisite

- Targeted machine should be Ubuntu 18.04+.
- Ansible has been installed.
    - If not, please check this [tutorial](https://www.digitalocean.com/community/tutorials/how-to-install-and-configure-ansible-on-ubuntu-18-04) to know how to install this Ansible.
- Create devops user on targeted machine (Ansible control node).
- Ensure the devops user has root permission with `sudo`.
- Ensure it can use the SSH Key to connect remote machine with devops user.

# How to create a devops user and configure current SSH key?

- Run `sudo useradd devops -s /bin/bash -m` to create the `devops` user.
- Run `echo "devops ALL=(ALL) NOPASSWD:ALL" | sudo tee /etc/sudoers.d/devops` to use sudo without password authentication.
- Run `ssh-keygen -t rsa -b 4096 -f /path/to/ssh_key -q -N ""` to create a SSH private/public Key.
- Run `ssh-copy-id -i /path/to/ssh_key.pub devops@$(hostname) -p port_number` to upload SSH public key to devops user.

# Usage

- Configure own `ansible.cfg` and `inventory` files on this current repository root folder.
- Run `ansible-playbook apt_upgrade.yml` command to setup Kuberenetes workers.

# References

- https://www.toptechskills.com/ansible-tutorials-courses/how-to-fix-usr-bin-python-not-found-error-tutorial
- https://www.cyberciti.biz/faq/ansible-apt-update-all-packages-on-ubuntu-debian-linux/
