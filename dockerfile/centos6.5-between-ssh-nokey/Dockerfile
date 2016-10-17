FROM    centos:6


RUN   yum    install   -y     sudo  openssh   openssh-server    openssh-clients   vim  htop    &&       mkdir  -p /var/run/sshd  &&   ssh-keygen -t rsa -f /etc/ssh/ssh_host_rsa_key  &&   ssh-keygen -t dsa -f /etc/ssh/ssh_host_dsa_key

RUN    useradd pbs    &&    su  pbs   &&   mkdir  -p   /home/pbs/.ssh   &&     ssh-keygen -q -N "" -t rsa -f  /home/pbs/.ssh/id_rsa &&  cp    /home/pbs/.ssh/id_rsa.pub   /home/pbs/.ssh/authorized_keys && chmod 644   /home/pbs/.ssh/authorized_keys && chown  -R   pbs:pbs   /home/pbs/  &&   chmod   700  /home/pbs/.ssh  &&  chmod  600  /home/pbs/.ssh/id_rsa



RUN   sed -i \
	-e 's~^#UseDNS yes~UseDNS no~g' \
	/etc/ssh/sshd_config

RUN   sed -i \
	-e 's/^#   StrictHostKeyChecking ask/StrictHostKeyChecking no/g' \
        -e 's/GSSAPIAuthentication yes/GSSAPIAuthentication no/g' \
        /etc/ssh/ssh_config

EXPOSE 22

ENTRYPOINT   ["/usr/sbin/sshd","-D"]
