# ansible_hadoop
### Installation

```sh
$ git clone https://github.com/Auster/ansible_hadoop.git
```

```sh
$ cd ./roles/hadoop/files/
$ wget http://www.eu.apache.org/dist/hadoop/common/hadoop-2.6.0/hadoop-2.6.0.tar.gz
$ cd ../../../
```

``` sh
$ cd ./roles/java/files/
$ curl -LO -H "Cookie: oraclelicense=accept-securebackup-cookie" "http://download.oracle.com/otn-pub/java/jdk/8u91-b14/jdk-8u91-linux-x64.tar.gz"
$ cd ../../../
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
```
