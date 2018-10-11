기본 정리

Host Computer - 현재 내가 사용하고 있는 컴퓨터(Windows/Mac/Linux)

Virtual Machine(Local FS) 

HDFS



### VM에 접속하기

```bash
$ ssh maria_dev@localhost -p 2222
```



### HDFS

```bash
# 둘 다 가능
$ hdfs dfs
$ hadoop fs
```



파일 확인하기

```bash
$ hdfs dfs -ls
```



새로운 디렉토리 생성

```bash
$ hdfs dfs -mkdir 디렉토리명
```



### 파일 복사하기

host -> VM -> HDFS

1. host에서 VM으로 파일 복사

```bash
$ scp -P 2222 ml-latest/* maria_dev@localhost:/home/maria_dev/data
```

host computer의 ml-latest 디렉토리 아래의 모든 파일을 VM의 home/maria_dev/data 디렉토리로 복사하라는 명령어



2. VM에서 HDFS로 파일 복사

```bash
$ hdfs dfs -copyFromLocal * ml-latest
```

현재 VM 디렉토리에 있는 파일을 ml-latest로 복사하라는 명령어