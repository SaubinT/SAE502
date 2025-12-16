FROM ubuntu:22.04

ENV DEBIAN_FRONTEND=noninteractive

RUN apt update && apt install -y \
    openssh-server sudo python3 \
    iputils-ping curl wget \
    rsync snmpd apache2

RUN mkdir /var/run/sshd

RUN useradd -ms /bin/bash ansible \
    && echo "ansible:ansible" | chpasswd \
    && usermod -aG sudo ansible \
    && echo "ansible ALL=(ALL) NOPASSWD:ALL" >> /etc/sudoers

EXPOSE 22

CMD ["/usr/sbin/sshd", "-D"]
