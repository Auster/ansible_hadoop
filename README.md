# ansible_hadoop
### Installation

```sh
$ git clone https://github.com/Auster/ansible_hadoop.git
$ cd ./ansible_hadoop
$ wget http://www.eu.apache.org/dist/hadoop/common/hadoop-2.6.0/hadoop-2.6.0.tar.gz -P ./roles/hadoop/files/
$ wget http://apache-mirror.rbc.ru/pub/apache/hbase/hbase-1.0.3/hbase-1.0.3-bin.tar.gz -P ./roles/hadoop/files/
$ cd ./roles/java/files/
$ curl -LO -H "Cookie: oraclelicense=accept-securebackup-cookie" "http://download.oracle.com/otn-pub/java/jdk/8u91-b14/jdk-8u91-linux-x64.tar.gz"
```
``` sh
$ vim ./hadoop_nodes.yaml
```

### Run playbook
```sh
$ ansible-playbook ./playbook.yml -i ./hadoop_nodes.yaml
```

### Run Hadoop
```sh
$ ssh user@master-node
$ su - hadoop
$ hdfs namenode -format
$ start-dfs.sh
$ start-yarn.sh
```

### Try Hadoop
```sh
$ yarn jar ~/share/hadoop/mapreduce/hadoop-mapreduce-examples-2.6.0.jar pi 16 10000
```

### Run HBase
```sh
$ su - hadoop
$ /opt/hbase/hbase-1.0.3/bin/start-hbase.sh
```

### Try HBase
```sh
$ /opt/hbase/hbase-1.0.3/bin/hbase shell
> create 'test', 'cf'
> list 'test'
> put 'test', 'row1', 'cf:a', 'value1'
> scan 'test'
> get 'test', 'row1'
> drop 'test'
```

### Options
./playbook.yml
```yaml
---
- roles:
   - java
  vars:
   - java_version_major: 8
   - java_version_minor: 91
   - java_home: "/opt/java"
   - java_archive_file_force_copy: 'yes'

- roles:
   - hadoop
  vars:
   - hadoop_version: '2.6.0'
   - hadoop_user: 'hadoop'
   - hadoop_home: '/opt/hadoop'
   - hadoop_data_dir: '/opt/hadoop/datadir'
   - hadoop_name_dir: '/opt/hadoop/namedir'
   - hadoop_archive_file_force_copy: 'no'
   - hadoop_master_as_slave: True
   
   - install_hbase: True
   - hbase_version: '1.0.3'
   - hbase_home: /opt/hbase
   - hbase_root_dir: "hdfs://HADOOP_MASTER:9000/hbase"
   - hbase_archive_file_force_copy: 'no'
   - hbase_zookeeper_data_dir: /opt/hbase/zookeeper/
```
