FROM centos:7
MAINTAINER andrzej.kardas
RUN rm -rf /etc/yum.repos.d/*
COPY centos.repo /etc/yum.repos.d/
RUN mkdir -p /deployment/cache && \
    yum -y update && \
    yum install -y java-1.8.0-openjdk-headless && \
    yum install -y telnet bind-utils tcpdump net-tools nmap-ncat iproute  &&  \
    yum clean all && \
    useradd -s /sbin/nologin -d /deployment javarunner 
COPY embedded-0.1-SNAPSHOT.jar /deployment/embedded.jar
RUN chown -R javarunner. /deployment
WORKDIR /deployment
USER javarunner
EXPOSE 5071
EXPOSE 8080
VOLUME [ "/deployment/cache" ]
ENTRYPOINT [ "/usr/bin/java", "-jar", "-Dhazelcast.config=/deployment/cache/hazelcast.xml" ,"/deployment/embedded.jar"]

