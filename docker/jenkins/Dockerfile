# Jenkins
#
# VERSION 0.0.1
# Authoer: kennylee26
# NAME: kennylee26/jenkins
# Command format: Instruction [arguments command] ..

# 第一行必须指定基于的基础镜像
FROM registry.alauda.cn/kenny/docker-jenkinsci:2.19.3

# 维护者信息
MAINTAINER kennylee26 <kennylee26@gmail.com>

USER root
RUN sed -i 's/archive.ubuntu.com/mirrors.163.com/g' /etc/apt/sources.list
RUN apt-get -y update
# recommend
RUN apt-get install -y \
      curl git unzip vim wget
# this image required
RUN apt-get install -y ant
# clean
RUN rm -rf /var/lib/apt/lists/*

# for main web interface:
EXPOSE 8080
# will be used by attached slave agents:
EXPOSE 50000

#COPY plugins.txt /usr/share/jenkins/plugins.txt
#RUN /usr/local/bin/plugins.sh /usr/share/jenkins/plugins.txt

ENTRYPOINT ["/bin/tini", "--", "/usr/local/bin/jenkins.sh"]
