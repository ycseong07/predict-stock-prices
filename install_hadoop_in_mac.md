# predict-stock-prices
Predicting stock price in real time using Hive and Python
It's not necessary for ML with pyspark in docker container. Follow the below if you want to do your projects on your local mac.
(2022.03.05 Updated)

## Hadoop install on Mac M1

### Prerequisites: homebrew, vscode, git, maven, java 11
Check local Java path with:
```
/usr/libexec/java_home
```
### Install Hadoop and Hive

Install Hadoop and Hive:

```shell
$ brew install hadoop
$ brew install hive
```

### Edit Hadoop configuration files

```shell
$ cd /opt/homebrew/Cellar/hadoop/3.3.2/libexec/etc/hadoop
```

1) Add to hadoop-env.sh the JAVA_HOME path:

```shell
export JAVA_HOME=/Library/Java/JavaVirtualMachines/adoptopenjdk-11.jdk/Contents/Home
```

2) Edit core-site.xml:

```xml
<configuration>
 <property>
  <name>fs.defaultFS</name>
  <value>hdfs://localhost:9000</value>
 </property>
</configuration>
```

3) Edit hdfs-site.xml:

```xml
<configuration>
  <property>
    <name>dfs.replication</name>
    <value>1</value>
  </property>
</configuration>
```

4) Edit mapred-site.xml:

```xml
<configuration>
    <property>
       <name>mapreduce.framework.name</name>
       <value>yarn</value>
    </property>
    <property>
    <name>mapreduce.application.classpath</name>   
  <value>
$HADOOP_MAPRED_HOME/share/hadoop/mapreduce/*:$HADOOP_MAPRED_HOME/share/hadoop/mapreduce/lib/*
  </value>
    </property>
</configuration>
```

5) Edit yarn-site.xml:

```xml
<configuration>
  <property>
    <name>yarn.nodemanager.aux-services</name>
    <value>mapreduce_shuffle</value>
  </property>
  <property>
    <name>yarn.nodemanager.env-whitelist</name>  
   <value>
JAVA_HOME,HADOOP_COMMON_HOME,HADOOP_HDFS_HOME,HADOOP_CONF_DIR,CLASSPATH_PREPEND_DISTCACHE,HADOOP_YARN_HOME,HADOOP_MAPRED_HOME
  </value>
  </property>
</configuration>
```

Update your ~/.bash_profile PATH:

```shell
PATH=$PATH:/opt/homebrew/Cellar/hadoop/3.3.2/sbin
```

Source your ~/.bash_profile

```shell
$ source ~/.bash_profile
```

### SSH Authentication

Generate new keygen and registeration:
```
ssh-keygen -t rsa -P '' -f ~/.ssh/id_rsa
cat ~/.ssh/id_rsa.pub >> ~/.ssh/authorized_keys
```

### Start / Stop Hadoop
```shell
# format HDFS
$ hadoop namenode -format
# unleash the Hadoop daemons
$ start-all.sh
```

Make sure all Hadoop processes started correctly:

```shell
$ jps
26564 Jps
25812 NameNode
26238 ResourceManager
26335 NodeManager
26047 SecondaryNameNode
```

Check if Hadoop works in localhost:9870

Stop Hadoop:

```shell
$ stop-all.sh
```

## References
https://stackoverflow.com/questions/48978480/hadoop-permission-denied-publickey-password-keyboard-interactive-warning  
https://codewitharjun.medium.com/install-hadoop-on-macos-efe7c860c3ed  
https://github.com/iizrailevsky/hadoop-hello-world

