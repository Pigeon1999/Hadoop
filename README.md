# Hadoop
하둡 공부 정리

# 개발환경 
window 10
java-1.8

# 3가지 실행 모드
하둡에는 3가지 실행 모드가 있습니다. 
- 독립 실행 모드(default) : 하둡이 설치된 로컬에서만 실행되기 때문에 로컬모드라고 부릅니다.
- 가상 분산 모드 : 하나의 장비에 모든 하둡 환경설정을 하고 하둡 서비스도 이 장비에서만 제공하는 방식입니다.
- 완전 분산 모드 : 여러 대의 장비에 하둡이 설치된 경우입니다. 하둡으로 라이브 서비스를 하게된 경우 이와 같은 방식으로 구성합니다. 

# 하둡 설치 방법 
#### 해당 블로그들을 참고 했습니다. 
https://codedragon.tistory.com/9582  
https://gist.github.com/vorpal56/5e2b67b6be3a827b85ac82a63a5b3b2e
https://github.com/cdarlint/winutils --> hadoop.dll 파일 다운로드 
https://github.com/steveloughran/winutils/blob/master/hadoop-2.7.1/bin/winutils.exe --> winutils.exe 파일 다운로드 
1. 아파치 하둡 사이트에서 다운로드 받습니다. binary download (https://hadoop.apache.org/)
2. 다운로드 받은 파일을 압축해제 합니다. tar.gz파일 입니다.  
#### [HDFS configurations]
3. hadoop-x.y.z\etc\hadoop 폴더에 있는 hadoop-env.cmd 파일을 열어 가장 아래에 코드를 추가합니다.
```
set HADOOP_PREFIX=%HADOOP_HOME%
set HADOOP_CONF_DIR=%HADOOP_PREFIX%\etc\hadoop
set YARN_CONF_DIR=%HADOOP_CONF_DIR%
set PATH=%PATH%;%HADOOP_PREFIX%\bin
```
4. core-site.xml을 열어 <configuration>태크 안에 코드를 추가합니다.
```
<configuration>
<property>
<name>fs.default.name</name>
<value>hdfs://0.0.0.0:19000</value>
</property>
</configuration>
```
5. hadoop-x.y.z폴더로 돌아와서 data폴더를 생성합니다.
6. data폴더안에 namenode, datanode폴더를 생성합니다.
7. 다시 etc\hadoop폴더로 가서 hdfs-site.xml을 열어 <configuration>태그안에 코드를 추가합니다.
```
<configuration>

<property>
<name>dfs.replication</name>
<value>1</value>
</property>

<property>
<name>dfs.name.dir</name>
<value>file:///D:/Hadoop/hadoop-3.3.6/data/namenode</value>
</property>

<property>
<name>dfs.data.dir</name>
<value>file:///D:/Hadoop/hadoop-3.3.6/data/datanode</value>
</property>

</configuration>
```
#### [YARN configurations]
8. mapred-site.xml파일을 열어 <configuration>태그안에 코드를 추가합니다.
```
<configuration>

<property>
<name>mapreduce.framework.name</name>
<value>yarn</value>
</property>

<property>
<name>mapreduce.jobtracker.adress</name>
<value>local</value>
</property>

</configuration>
```
9. yarn-site.xml파일을 열어 <configuration>태그안에 코드를 추가합니다.
```
<configuration>
 
<!-- Site specific YARN configuration properties -->
<property>
<name>yarn.server.resourcemanager.address</name>
<value>0.0.0.0:8020</value>
</property>
 
 
<property>
<name>yarn.server.resourcemanager.application.expiry.interval</name>
<value>60000</value>
</property>
 
 
<property>
<name>yarn.server.nodemanager.address</name>
<value>0.0.0.0:45454</value>
</property>
 
 
<property>
<name>yarn.nodemanager.aux-services</name>
<value>mapreduce_shuffle</value>
</property>
<property>
<name>yarn.nodemanager.aux-services.mapreduce.shuffle.class</name>
<value>org.apache.hadoop.mapred.ShuffleHandler</value>
</property>
 
 
<property>
<name>yarn.server.nodemanager.remote-app-log-dir</name>
<value>/app-logs</value>
</property>
 
 
<property>
<name>yarn.nodemanager.log-dirs</name>
<value>/dep/logs/userlogs</value>
</property>
 
 
<property>
<name>yarn.server.mapreduce-appmanager.attempt-listener.bindAddress</name>
<value>0.0.0.0</value>
</property>
 
 
<property>
<name>yarn.server.mapreduce-appmanager.client-service.bindAddress</name>
<value>0.0.0.0</value>
</property>
 
 
<property>
<name>yarn.log-aggregation-enable</name>
<value>true</value>
</property>
 
 
<property>
<name>yarn.log-aggregation.retain-seconds</name>
<value>-1</value>
</property>
 
 
<property>
<name>yarn.application.classpath</name>
<value>%HADOOP_CONF_DIR%,%HADOOP_COMMON_HOME%/share/hadoop/common/*,%HADOOP_COMMON_HOME%/share/hadoop/common/lib/*,%HADOOP_HDFS_HOME%/share/hadoop/hdfs/*,%HADOOP_HDFS_HOME%/share/hadoop/hdfs/lib/*,%HADOOP_MAPRED_HOME%/share/hadoop/mapreduce/*,%HADOOP_MAPRED_HOME%/share/hadoop/mapreduce/lib/*,%HADOOP_YARN_HOME%/share/hadoop/yarn/*,%HADOOP_YARN_HOME%/share/hadoop/yarn/lib/*</value>
</property>
 
</configuration>
```

#### [Initialize environment variables]
10. cmd를 실행하고, 환경변수를 설정해주는 hadoop-env.cmd 파일이 있는 위치로 이동하고 실행합니다.
![image](https://github.com/Pigeon1999/Hadoop/assets/98893114/d818297e-6201-45e4-beaa-48f38ffa153a)
11. 파일 시스템을 포맷합니다.
```
hadoop namenode -format
```
또는 
```
hdfs namenode -format
```
12. hadoop.dll 파일과 winutils.exe 파일을 다운로드해서 bin폴더에 넣습니다. 
13. HDFS 데몬을 실행합니다. 실행시 두개의 명령어 창이 오픈되는데, 각각 namenode와 datanode입니다.
```
%HADOOP_HOME%\sbin\start-dfs.cmd
```
14. YARN 데몬을 실행합니다. 실행하면 총 4개의 cmd창이 실행됩니다. 각각 namenode, datanode, YARN resource manager, YARN node manager입니다.
```
%HADOOP_HOME%\sbin\start-yarn.cmd
```
![image](https://github.com/Pigeon1999/Hadoop/assets/98893114/80d89459-60ae-4e95-9f0e-f635e7fbe3bd)  
* nodemanager는 실시간으로 출력


#### [Resource manager 오픈]
15. YARN 웹사이트를 통해서 job status를 확인할 수 있습니다. (http://localhost:8088)
    
