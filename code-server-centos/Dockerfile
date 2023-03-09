FROM centos

RUN ln -snf /usr/share/zoneinfo/$TIME_ZONE /etc/localtime

ENV TIME_ZONE Asia/Shanghai

RUN sed -i 's/mirrorlist/#mirrorlist/g' /etc/yum.repos.d/CentOS-* \
  && sed -i 's|#baseurl=http://mirror.centos.org|baseurl=http://vault.centos.org|g' /etc/yum.repos.d/CentOS-* \
  && yum -y update \
  && yum -y install \
    vim \
    curl \
    sudo \
    git

COPY install.sh /root

RUN sh /root/install.sh && rm -f /root/install.sh

RUN adduser coder && echo "coder ALL=(ALL) NOPASSWD:ALL" >> /etc/sudoers.d/nopasswd

USER coder

WORKDIR /home/coder

ENTRYPOINT ["code-server", "--bind-addr", "0.0.0.0:8080", "."]
