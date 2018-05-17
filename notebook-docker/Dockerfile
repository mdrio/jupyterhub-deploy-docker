#docker build  -t notebook .
FROM jupyter/minimal-notebook

WORKDIR /home/jovyan
ENV HADOOP_VERSION=2.8.3
RUN wget http://mirror.nohup.it/apache/hadoop/common/hadoop-${HADOOP_VERSION}/hadoop-${HADOOP_VERSION}.tar.gz && \
    tar xf hadoop-${HADOOP_VERSION}.tar.gz 
ENV HADOOP_HOME=/home/jovyan/hadoop-${HADOOP_VERSION}

ENV JAVA_HOME=/usr/lib/jvm/java-8-openjdk-amd64
RUN	echo "<?xml version=\"1.0\"?><?xml-stylesheet type=\"text/xsl\" href=\"configuration.xsl\"?><configuration><property><name>yarn.nodemanager.bind-host</name><value>0.0.0.0</value></property><property><name>mapreduce.framework.name</name><value>yarn</value></property></configuration>" > ${HADOOP_HOME}/etc/hadoop/mapred-site.xml && \
	echo "<?xml version=\"1.0\" encoding=\"UTF-8\"?><?xml-stylesheet type=\"text/xsl\" href=\"configuration.xsl\"?><configuration><property><name>dfs.client.use.datanode.hostname</name><value>true</value></property></configuration>" > ${HADOOP_HOME}/etc/hadoop/hdfs-site.xml && \
	echo "<?xml version=\"1.0\" encoding=\"UTF-8\"?><?xml-stylesheet type=\"text/xsl\" href=\"configuration.xsl\"?><configuration><property><name>fs.defaultFS</name><value>hdfs://NAMENODE:8020</value></property></configuration>" > ${HADOOP_HOME}/etc/hadoop/core-site.xml

USER root
RUN     apt update && apt install -yq  openjdk-8-jdk && \
        pip install --pre pydoop && \
        pip install pyspark pandas matplotlib bokeh 

USER jovyan


WORKDIR /home/jovyan/work


