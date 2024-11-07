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
# Installation of OpenSSH server
########

RUN apt-get install -y openssh-server
RUN mkdir /var/run/sshd
RUN echo 'root:root' |chpasswd
RUN sed -ri 's/^#?PermitRootLogin\s+.*/PermitRootLogin yes/' /etc/ssh/sshd_config
RUN sed -ri 's/UsePAM yes/#UsePAM yes/g' /etc/ssh/sshd_config

RUN touch /root/.ssh/authorized_keys
RUN echo 'ssh-ed25519 AAAAC3NzaC1lZDI1NTE5AAAAIPvbHGC1gvB6SFWzxICovpcp12yVmG2b5BQAsqABdqYe root@localhost' > /root/.ssh/authorized_keys
RUN chmod 700 /root/.ssh && chmod 600 /root/.ssh/authorized_keys

########
# Preparation for Ansible connections
########

RUN apt install -y python3 python3-pip

########
# Clean up
########

RUN apt-get clean && \
    rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

EXPOSE 22
CMD ["/usr/sbin/sshd", "-D"]
