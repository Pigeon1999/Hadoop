# Hadoop
하둡 공부 정리

# 하둡 설치 방법 
1. 아파치 하둡 사이트에서 다운로드 받습니다. binary download (https://hadoop.apache.org/)
2. 다운로드 받은 파일을 압축해제 합니다. tar.gz파일 입니다.
3. hadoop\etc\hadoop 폴더에 있는 hadoop-env.cmd 파일을 열어 가장 아래에 코드를 추가합니다.

```
set HADOOP_PREFIX=%HADOOP_HOME%
set HADOOP_CONF_DIR=%HADOOP_PREFIX%\etc\hadoop
set YARN_CONF_DIR=%HADOOP_CONF_DIR%
set PATH=%PATH%;%HADOOP_PREFIX%\bin
```

