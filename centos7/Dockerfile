FROM centos

RUN yum -y install openssh-server

RUN useradd remote_user && \
    echo "remote_user:123456" | chpasswd && \
    mkdir /home/remote_user/.ssh && \
    chmod 700 /home/remote_user/.ssh

COPY remote-key.pub /home/remote_user/.ssh/authorized_keys

RUN chown remote_user:remote_user   -R /home/remote_user && \
    chmod 600 /home/remote_user/.ssh/authorized_keys

RUN ssh-keygen -A

RUN yum -y install mysql

RUN yum install -y python3

RUN curl "https://bootstrap.pypa.io/get-pip.py" -o "get-pip.py" && \
	python3 get-pip.py && \
	pip install awscli --upgrade
RUN rm -rf /run/nologin

CMD /usr/sbin/sshd -D
