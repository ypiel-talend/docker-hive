## Apache Hadoop and Hive

Docker image to setup Apache Hadoop and Hive using derby as metastore backend.


### Version

* Oracle Java 8
* Apache Hadoop - 2.7.2
* Apache Hive - 2.1.0


### Setup

1. Install [docker](https://docs.docker.com/docker-for-mac/)
2. Execute to start Hive CLI
    ```
    docker run -i -p 10000:10000 -v /tmp/share_dir/:/tmp/share_dir -t hive /bin/bash
    ```
3. Into the container
    ```
    cd /usr/local/hadoop
    cp share/hadoop/common/hadoop-common-2.7.6.jar /tmp/share_dir
    cd /usr/local/hive
    tar -czf /tmp/share_dir/hive.libs.tgz ./lib/
    schematool -dbType derby -initSchema
    hiveserver2
    ```
4. Connect within Squirrel
	* Add new driver
	* Name : Hive
	* Example URL : jdbc:hive2://localhost:10000/default
	* Extra Class Path : unzip jars from /tmp/shared_dir/hive.libs.tgz and select jars + hadoop-common
	* Class name : org.apache.hive.jdbc.HiveDriver
	* In 'Aliases' creater new aliases and select Hive driver
	* User Name : APP
	* Let password empty
