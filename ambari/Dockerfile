#   Licensed under the Apache License, Version 2.0 (the "License");
#   you may not use this file except in compliance with the License.
#   You may obtain a copy of the License at
#
#       http://www.apache.org/licenses/LICENSE-2.0
#
#   Unless required by applicable law or agreed to in writing, software
#   distributed under the License is distributed on an "AS IS" BASIS,
#   WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
#   See the License for the specific language governing permissions and
#   limitations under the License.

FROM centos:centos6

RUN echo root:changeme | chpasswd
ENV HOME /root

## Install some basic utilities that aren't in the default image
RUN yum clean all -y && yum update -y && yum install -y install vim \
    wget \
    rpm-build \
    sudo \
    which \
    telnet \
    tar \
    openssh-server \
    openssh-clients \
    ntp \
    git \
    python-setuptools \
    python-devel \
    httpd \
# phantomjs dependency
    fontconfig \
    freetype \
    libfreetype.so.6 \
    libfontconfig.so.1 \
    libstdc++.so.6 \
    gcc-g++ \
    gcc \
    make
RUN rpm -e --nodeps --justdb glibc-common
RUN yum -y install glibc-common


#Install JAVA
RUN wget --header "Cookie: oraclelicense=accept-securebackup-cookie" http://download.oracle.com/otn-pub/java/jdk/8u144-b01/090f390dda5b47b9b721c7dfaa008135/jdk-8u144-linux-x64.rpm
RUN rpm -ivh jdk-8u144-linux-x64.rpm
ENV JAVA_HOME /usr/java/default/

#Install Maven
RUN mkdir -p /opt/maven
WORKDIR /opt/maven
RUN wget http://apache.cs.utah.edu/maven/maven-3/3.5.0/binaries/apache-maven-3.5.0-bin.tar.gz
RUN tar -xvzf /opt/maven/apache-maven-3.5.0-bin.tar.gz
RUN rm -rf /opt/maven/apache-maven-3.5.0-bin.tar.gz

ENV M2_HOME /opt/maven/apache-maven-3.5.0
ENV PATH "$PATH:$JAVA_HOME/bin:$M2_HOME/bin"


# SSH key
RUN ssh-keygen -f /root/.ssh/id_rsa -t rsa -N ''
RUN cat /root/.ssh/id_rsa.pub > /root/.ssh/authorized_keys
RUN chmod 600 /root/.ssh/authorized_keys
RUN sed -ri 's/UsePAM yes/UsePAM no/g' /etc/ssh/sshd_config

#To allow bower install behind proxy. See https://github.com/bower/bower/issues/731
RUN git config --global url."https://".insteadOf git://

# Install python, nodejs and npm
RUN curl --silent --location https://rpm.nodesource.com/setup_6.x | bash -
RUN yum clean all && yum install -y nodejs
RUN npm install -g npm@latest
#RUN npm install -g brunch@1.7.20

# Once run some mvn commands to cache .m2/repository
WORKDIR /tmp
#RUN git clone https://github.com/apache/ambari.git
#WORKDIR /tmp/ambari

#RUN mvn -B -X clean install package rpm:rpm -DskipTests -Dpython.ver="python >= 2.6" -Preplaceurl

