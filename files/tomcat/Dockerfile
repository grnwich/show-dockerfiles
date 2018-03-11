#版本信息
FROM centos
MAINTAINER locutus "grnwich@163.com"


# OS环境配置
RUN yum install -y wget


#安装JDK，因为JDK下载很麻烦，所以直接用拷贝比较快
RUN mkdir /var/tmp/jdk
COPY jdk-8u161-linux-x64.tar.gz /var/tmp/jdk
RUN tar xzf /var/tmp/jdk/jdk-8u161-linux-x64.tar.gz -C /var/tmp/jdk \
    && rm -rf /var/tmp/jdk/jdk-8u161-linux-x64.tar.gz


#安装tomcat
RUN mkdir /var/tmp/tomcat
COPY apache-tomcat-8.0.49.tar.gz /var/tmp/tomcat
RUN tar xzf \
    /var/tmp/tomcat/apache-tomcat-8.0.49.tar.gz \
    -C /var/tmp/tomcat && rm -rf \
    /var/tmp/tomcat/apache-tomcat-8.0.49.tar.gz


#设置环境变量
ENV JAVA_HOME /var/tmp/jdk/jdk1.8.0_161
ENV CATALINA_HOME /var/tmp/tomcat/apache-tomcat-8.0.49
ENV PATH $PATH:$JAVA_HOME/bin:$CATALINA_HOME/bin

#打包项目并拷贝到tomcat webapps目录
RUN mkdir /var/tmp/webapp
ADD ./  /var/tmp/webapp
#RUN cd  /var/tmp/webapp  \
#    && cp /Users/cos/software/delvsoftware/apache-tomcat-7.0.70/webapps/ROOT.war \
#    /var/tmp/tomcat/apache-tomcat-8.0.49/webapps/


#开启内部服务端口
EXPOSE 8080

#启动tomcat服务器
CMD ["./var/tmp/tomcat/apache-tomcat-8.0.49/bin/catalina.sh","run"] \
    && tail -f /var/tmp/tomcat/apache-tomcat-8.0.49/logs/catalina.out
