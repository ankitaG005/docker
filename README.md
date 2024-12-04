# docker

1  for pkg in docker.io docker-doc docker-compose docker-compose-v2 podman-docker containerd runc; do sudo apt-get remove $pkg; done
    2  # Add Docker's official GPG key:
    3  sudo apt-get update
    4  sudo apt-get install ca-certificates curl
    5  sudo install -m 0755 -d /etc/apt/keyrings
    6  sudo curl -fsSL https://download.docker.com/linux/ubuntu/gpg -o /etc/apt/keyrings/docker.asc
    7  sudo chmod a+r /etc/apt/keyrings/docker.asc
    8  # Add the repository to Apt sources:
    9  echo   "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.asc] https://download.docker.com/linux/ubuntu \
       $(. /etc/os-release && echo "$VERSION_CODENAME") stable" |   sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
   10  sudo apt-get update
   11  sudo apt-get install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
   12  sudo apt install openjdk-17-jdk
   13  java --version
   14  ssh-keygen
   15  cd .ssh
   16  ls
   17  cat id_ed25519
   18  cat id_ed25519.pub
   19  sudo vi authorized_keys 
   20  cd /homo/ubuntu
   21  cd /home/ubuntu
   22  mkdir jenkins
   23  cd jenkins/
   24  pwd
   25  sudo docker ps


   #hkhcoder/vrofile
   https://github.com/hkhcoder/vprofile-project.git

   #Ansible
   $ sudo apt update
   $ sudo apt install software-properties-common
   $ sudo add-apt-repository --yes --update ppa:ansible/ansible
   $ sudo apt install ansible
