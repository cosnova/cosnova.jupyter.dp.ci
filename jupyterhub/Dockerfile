FROM jupyter/tensorflow-notebook:latest

USER root
RUN apt-get update && apt-get upgrade 
RUN apt-get -y install curl
RUN apt-get -y install kafkacat

RUN apt-get -y install default-jdk scala git openjdk-8-jdk
RUN wget https://archive.apache.org/dist/spark/spark-2.4.6/spark-2.4.6-bin-hadoop2.7.tgz
RUN tar xvf spark-*
RUN mv spark-2.4.6-bin-hadoop2.7 /opt/spark
RUN echo "export SPARK_HOME=/opt/spark" >> ~/.profile && echo "export PATH=$PATH:$SPARK_HOME/bin:$SPARK_HOME/sbin" >> ~/.profile && echo "export PYSPARK_PYTHON=/usr/bin/python3" >> ~/.profile && source ~/.profile
RUN echo "export PATH=/opt/conda/bin:/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/bin:/sbin:/opt/spark/bin:/opt/spark/sbin" >> ~/.profile && echo "export PYSPARK_PYTHON=/usr/bin/python3" >> ~/.profile && echo "export JAVA_HOME=/usr/lib/jvm/java-8-openjdk-amd64/" >> ~/.profile && source ~/.profile
RUN echo "export PYSPARK_SUBMIT_ARGS='--packages org.apache.spark:spark-sql-kafka-0-10_2.11:2.4.6,org.apache.spark:spark-streaming-kafka-0-10-assembly_2.12-2.4.6,org.apache.kafka:kafka-clients:0.10.1.0 pyspark-s$'" >> ~/.profile && source ~/.profile
RUN wget https://repo1.maven.org/maven2/org/apache/spark/spark-streaming-kafka-0-10-assembly_2.12/2.4.6/spark-streaming-kafka-0-10-assembly_2.12-2.4.6.jar -P /opt/spark/lib
RUN wget https://repo1.maven.org/maven2/org/apache/kafka/kafka-clients/0.10.1.0/kafka-clients-0.10.1.0.jar -P /opt/spark/lib
RUN wget https://repo1.maven.org/maven2/org/postgresql/postgresql/42.2.16/postgresql-42.2.16.jar -P /opt/spark/lib
RUN wget https://repo1.maven.org/maven2/org/apache/spark/spark-sql-kafka-0-10_2.11/2.4.6/spark-sql-kafka-0-10_2.11-2.4.6.jar -P /opt/spark/lib

RUN apt-get install -yq git openssh-client recode && rm -rf /var/lib/apt/lists/*

RUN echo "jovyan ALL=(ALL) NOPASSWD:ALL" > /etc/sudoers.d/notebook


USER 1000
