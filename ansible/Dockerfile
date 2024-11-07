########
# https://4sysops.com/archives/how-to-deploy-ansible-inside-a-docker-container/
# https://github.com/rastasheep/ubuntu-sshd
########

FROM debian:bookworm

ENV DEBIAN_FRONTEND=noninteractive

########
# Update
########

RUN apt-get update

########
# Installation of OpenSSH client
########

RUN apt-get install -y openssh-client
RUN mkdir /root/.ssh

COPY ./id_ed25519 /root/.ssh/id_ed25519

RUN chmod 0600 /root/.ssh/id_ed25519
RUN eval "$(ssh-agent -s)" && ssh-add /root/.ssh/id_ed25519

########
# Installation of Ansible
########

RUN apt install -y gnupg vim
RUN echo "deb http://ppa.launchpad.net/ansible/ansible/ubuntu focal main" | tee /etc/apt/sources.list.d/ansible.list
RUN apt-key adv --keyserver keyserver.ubuntu.com --recv-keys 93C4A3FD7BB9C367
RUN apt update
RUN apt install -y ansible
RUN mkdir /etc/ansible

########
# Clean up
########

RUN apt-get clean && \
    rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

CMD ["tail", "-f", "/dev/null"]
