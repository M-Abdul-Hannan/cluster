##  Single_Node_Cluster(Hadoop 3)


##### connect to the Datacenter with Public_key or Private_key in case of windows (cmd,putty,vm,subsystem)

your key is in Downloads folder so fire command
```
cd Downloads/
```
## connect with the remote server first  
```
ssh -i file.pem ubuntu@public_ip
```
## Install Java
```
sudo apt-get update
```
```
sudo apt-get install openjdk-8-jdk openjdk-8-jre -y
```
```
java -version
```
## Create a Hadoop user for accessing HDFS and MapReduce
```
sudo addgroup hadoop
```

## create password after you fire the below command
```
sudo adduser hduser --ingroup hadoop
```
```     
sudo adduser hduser sudo
```
```
sudo su hduser
```
## Configure SSH
 Come out from the /home/ubuntu
```
cd
```
```
sudo su
```
```        
ssh-keygen
```
```
cd .ssh
```
```
cat id_rsa.pub >> authorized_keys
```
```
ssh localhost

```

# Download Hadoop
```
wget https://dlcdn.apache.org/hadoop/common/stable/hadoop-3.3.5.tar.gz

```
  * Extract and Install Hadoop tar ball

```
tar -xzvf hadoop-3.3.5.tar.gz
```
```
sudo mv hadoop-3.3.5 /usr/local/hadoop
```
```
sudo chown hduser:hadoop -R /usr/local/hadoop
```
## Set Enviornment Variable
```
readlink -f $(which java)
```
```
nano ~/.bashrc
```
 * copy and paste below code in last of the script

```
export JAVA_HOME=/usr/lib/jvm/java-8-openjdk-amd64 <br>
export HADOOP_HOME=/usr/local/hadoop <br>
export PATH=$PATH:$HADOOP_HOME/bin<br>
export PATH=$PATH:$HADOOP_HOME/sbin<br>
export PATH=$PATH:/usr/local/hadoop/bin/<br>
export HADOOP_MAPRED_HOME=$HADOOP_HOME<br>
export HADOOP_COMMON_HOME=$HADOOP_HOME<br>
export HADOOP_HDFS_HOME=$HADOOP_HOME<br>
export YARN_HOME=$HADOOP_HOME<br>
export HADOOP_CONF_DIR=/usr/local/hadoop/etc/hadoop
```

```
source ~/.bashrc
```
```
cd /usr/local/hadoop/etc/hadoop/
```
## Update hadoop-env.sh
```
nano hadoop-env.sh
```
```
export JAVA_HOME=/usr/lib/jvm/java-8-openjdk-amd64
export HADOOP_LOG_DIR=/var/log/hadoop
```
```
sudo mkdir /var/log/hadoop
```
```
sudo chown hduser:hadoop -R /var/log/hadoop
```
## Update core-site.xml
```
nano core-site.xml
```
```
 <property>
  <name>fs.defaultFS</name>
  <value>hdfs://localhost:54310</value>
 </property>
```

## Update mapred-site.xml
```
nano mapred-site.xml
```
```
<property>
  <name>mapreduce.jobtracker.address</name>
  <value>localhost:54311</value>
   </property>
<property>
   <name>mapreduce.framework.name</name>
   <value>yarn</value>
 </property>
<property>
  <name>yarn.app.mapreduce.am.env</name>
  <value>HADOOP_MAPRED_HOME=$HADOOP_MAPRED_HOME</value>
</property>
<property>
  <name>mapreduce.map.env</name>
  <value>HADOOP_MAPRED_HOME=$HADOOP_MAPRED_HOME</value>
</property>
<property>
  <name>mapreduce.reduce.env</name>
  <value>HADOOP_MAPRED_HOME=$HADOOP_MAPRED_HOME</value>
</property>
```

## Update hdfs-site.xml
```
sudo mkdir -p /usr/local/hadoop_store/hdfs/namenode
```
```
sudo mkdir -p /usr/local/hadoop_store/hdfs/datanode
```
```
sudo chown -R hduser:hadoop /usr/local/hadoop_store
```
```
nano hdfs-site.xml
```
```<property>
<name>dfs.replication</name>
  <value>1</value>
 </property>
 <property>
   <name>dfs.namenode.name.dir</name>
   <value>file:/usr/local/hadoop_store/hdfs/namenode</value>
 </property>
 <property>
   <name>dfs.datanode.data.dir</name>
   <value>file:/usr/local/hadoop_store/hdfs/datanode</value>
 </property>
```

## Update yarn-site.xml
```
nano yarn-site.xml
```
```
<property>
      <name>yarn.nodemanager.aux-services</name>
      <value>mapreduce_shuffle</value>
   </property>
<property>
        <name>yarn.nodemanager.env-whitelist</name>
        <value>JAVA_HOME,HADOOP_COMMON_HOME,HADOOP_HDFS_HOME,HADOOP_CONF_DIR,CLASSPATH_PREPEND_DISTCACHE,HADOOP_YARN_HOME,HADOOP_MAPRED_HOME</value>
  </property>
```

## Format Namenode
```
hdfs namenode -format
```
```
start-dfs.sh
```
```
start-yarn.sh
```
```
jps
```

## Lets do some work on it
```
hdfs dfs -mkdir /user
```
```
hdfs dfs -mkdir /user/hduser
```
```
hdfs dfs -put hadoop-3.3.5.tar.gz /user/hduser
```

## WebUI copy the ip_address of your instance and paste in the url  
```
 ip_address:9870
```
Active

## Click on utilities in that click on Browse the folder/directory
