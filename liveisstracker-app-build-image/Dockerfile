FROM openjdk:14-jdk-slim
MAINTAINER MANOJMANIVANNAN
RUN apt-get update \
	&& apt-get install -y python3 python3-pip \
	&& apt-get install -y wget git
RUN wget http://apachemirror.wuchna.com/maven/maven-3/3.6.3/binaries/apache-maven-3.6.3-bin.tar.gz
RUN tar -xzvf apache-maven-3.6.3-bin.tar.gz -C /opt && rm -f apache-maven-3.6.3-bin.tar.gz
RUN echo 'export M2_HOME=/opt/apache-maven-3.6.3/' >> ~/.bashrc
RUN echo 'export PATH=$PATH:$M2_HOME/bin' >> ~/.bashrc
RUN echo 'export TERM=dumb' >> ~/.bashrc
