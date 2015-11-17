FROM ansible/ubuntu14.04-ansible
MAINTAINER Trang TTTT<trang.tran@aalto.fi>

RUN mkdir /tests
VOLUME /vagrant/tests /tests

COPY script.sh /
CMD chmod +x /script.sh

ENV LCT /LCT-C
ENV LimeTB /LimeTB

ADD LCT-C-1.1.1.tar.gz ${LCT} 
ADD LimeTB-2.2.0.tar.gz ${LimeTB} 

RUN sudo apt-get install -y openssh-server

WORKDIR ${LCT}/LCT-C-1.1.1
#RUN sudo make llvm all

WORKDIR ${LimeTB}/LimeTB-2.2.0

COPY playbook.yml /etc/ansible/playbook.yml
COPY vagrant.pub /etc/ansible/vagrant.pub
RUN ansible-playbook /etc/ansible/playbook.yml --connection=local

RUN mkdir /var/run/sshd
RUN chmod 0755 /var/run/sshd
RUN sed 's@session\s*required\s*pam_loginuid.so@session optional pam_loginuid.so@g' -i /etc/pam.d/sshd

#RUN sudo /etc/init.d/ssh start
EXPOSE 22
#CMD ["sudo","/etc/init.d/ssh", "start"]
CMD ["/usr/sbin/sshd", "-D"]
