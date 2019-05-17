FROM ubuntu:16.04

ARG ssh_prv_key
ARG ssh_pub_key

RUN apt-get update && apt-get install -y openssh-server
RUN mkdir /var/run/sshd
RUN echo 'root:Atinuke001' | chpasswd
RUN sed -i 's/PermitRootLogin prohibit-password/PermitRootLogin yes/' /etc/ssh/sshd_config

# SSH login fix. Otherwise user is kicked off after login
 RUN sed 's@session\s*required\s*pam_loginuid.so@session optional pam_loginuid.so@g' -i /etc/pam.d/sshd

ENV NOTVISIBLE "in users profile"
RUN echo "export VISIBLE=now" >> /etc/profile
# Authorize SSH Host
RUN mkdir -p /root/.ssh && \
    chmod 0700 /root/.ssh && \
    ssh-keyscan github.com > /root/.ssh/known_hosts

# Add the keys and set permissions
# RUN echo "$ssh_prv_key" > /root/.ssh/id_rsa && \
  #  echo "$ssh_pub_key" > /root/.ssh/id_rsa.pub && \
  #  chmod 600 /root/.ssh/id_rsa && \
  #  chmod 600 /root/.ssh/id_rsa.pub

EXPOSE 22
CMD ["/usr/sbin/sshd", "-D"]
