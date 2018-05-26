# bigdata

# create hadoop user on all 3 nodes and add to wheel group for sudo
useradd hadoop
passwd hadoop
usermod -aG wheel hadoop

# /etc/hosts file on all systems should be
172.24.0.100 master.example.com master
172.24.0.101 node1.example.com node1
172.24.0.102 node2.example.com node2

# implement passwordless authentication
# on master
ssh-keygen -t rsa
ssh-copy-id hadoop@172.24.0.101
ssh-copy-id hadoop@172.24.0.102
ssh-copy-id hadoop@172.24.0.100
ssh hadoop@172.24.0.101
ssh hadoop@172.24.0.102




# set java variable on all 3 centos 7 nodes
# /etc/profile.d/java.sh
export JAVA_HOME=/usr/lib/jvm/java-1.8.0-openjdk-1.8.0.171-8.b10.el7_5.x86_64/jre
export JAVA_PATH=$JAVA_HOME
export PATH=$PATH:$JAVA_HOME/bin

# install java on all 3 centos 7 nodes
java -version
yum install java-1.8.0-openjdk
yum install java-1.8.0-openjdk-devel
update-alternatives --display java

# download, extract, rename on all 3 centos nodes
wget http://redrockdigimark.com/apachemirror/hadoop/common/hadoop-2.8.4/hadoop-2.8.4.tar.gz
tar -xfz hadoop-2.8.4.tar.gz
mv hadoop-2.8.4 hadoop

# edit core-site.xml, hdfs-site.xml, mapred-site.xml, yarn-site.xml

# scp hadoop tar.gz and 4 xml files to node1, node2
scp hadoop-*.tar.gz node1:/home/hadoop
scp hadoop-*.tar.gz node2:/home/hadoop
scp ~/hadoop/etc/hadoop/* node1:/home/hadoop/hadoop/etc/hadoop/
scp ~/hadoop/etc/hadoop/* node2:/home/hadoop/hadoop/etc/hadoop/





