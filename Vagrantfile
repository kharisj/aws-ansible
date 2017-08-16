# -*- mode: ruby -*-
# vi: set ft=ruby :
Vagrant.configure("2") do |config|
  # The most common configuration options are documented and commented below.
  # For a complete reference, please see the online documentation at
  # https://docs.vagrantup.com.
  # Every Vagrant development environment requires a box. You can search for
  # boxes at https://atlas.hashicorp.com/search.
  config.vm.box = "centos/7"
  config.vm.box_version = "1702.01"
  # config.vm.network "private_network", ip: "192.168.33.10"
  # config.vm.synced_folder "../data", "/vagrant_data"
  # Enable provisioning with a shell script. Additional provisioners such as
  # Puppet, Chef, Ansible, Salt, and Docker are also available. Please see the
  # documentation for more information about their specific syntax and use.
  # config.vm.provision "shell", inline: <<-SHELL
  #   apt-get update
  #   apt-get install -y apache2
  # SHELL
  config.vm.provision "shell", inline: <<-SHELL
    sudo yum update
    ansible --version
    if [ $? == 0 ]; then
       echo "Successfully install Ansible"
    else
       echo "Installing Ansible"
       sudo yum install -y epel-release
       sudo yum -y install gcc gcc-c++ kernel-devel python-devel libxslt-devel libffi-devel openssl-devel \
       python-pip python-wheel python-jinja2 pyOpenSSL python-lxml git
       sudo pip install --upgrade pip
       sudo pip install libselinux-python
       sudo pip install boto
       sudo pip install ansible # ==2.1.2.0
       echo "Ansible Installed Successful"
    fi
    sudo sed -e "s/#PermitRootLogin yes/PermitRootLogin yes/" \
    -e "s/PasswordAuthentication no/#PasswordAuthentication no/" \
    -e "s/#PasswordAuthentication yes/PasswordAuthentication yes/" \
    -i /etc/ssh/sshd_config
    systemctl restart sshd
    sudo mkdir -p /opt/openshift-ansible/
    sudo git clone https://github.com/openshift/openshift-ansible.git /opt/openshift-ansible/
  SHELL
end
