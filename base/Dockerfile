FROM armv7/armhf-ubuntu

#requirements
RUN apt-get update; apt-get install -y curl wget supervisor openssh-server openssh-client nano

#priviledge separation directory
RUN mkdir /var/run/sshd

#install Java 7 Oracle JDK
RUN mkdir -p /usr/java/default && \
   wget -q -O - https://github.com/nagarajjayakumar/docker-arm-flink/raw/master/jdk-8u65-linux-arm32-vfp-hflt.tar.gz | tar -zxvf - -C  /usr/java/default/

ENV JAVA_HOME /usr/java/default/jdk1.8.0_65/

#Install Java Open JDK
#RUN apt-get install -y unzip openjdk-7-jre-headless
#ENV JAVA_HOME=/usr/lib/jvm/java-7-openjdk-amd64/


RUN echo 'root:secret' | chpasswd

#SSH as root... probably needs to be revised for security!
RUN sed -i 's/PermitRootLogin without-password/PermitRootLogin yes/' /etc/ssh/sshd_config

EXPOSE 22

# supervisor base configuration
ADD supervisor.conf /etc/supervisor/

# default command / not overridable CMD needed for supervisord
#CMD ["supervisord", "-c", "/etc/supervisor.conf"]


