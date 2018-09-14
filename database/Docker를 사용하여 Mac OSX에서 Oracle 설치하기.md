# Docker를 사용하여 Mac OSX에서 Oracle 설치하기

### 자바가 설치되어있지 않은 경우

아래 링크에서 JDK 8 설치

꼭 8버전이어야 한다. 다른 버전은 안됨ㅠㅠ

http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html

![Screen Shot 2018-09-13 at 12.50.44 AM](/Users/seungyeonlee/Desktop/Screen%20Shot%202018-09-13%20at%2012.50.44%20AM.png)





## Docker 설치

https://store.docker.com/editions/community/docker-ce-desktop-mac

1. 중간 쯤으로 스크롤을 내려서 왼쪽에 있는 **stable version**을 다운로드

![Screen Shot 2018-09-13 at 12.32.37 AM](/Users/seungyeonlee/Desktop/Screen Shot 2018-09-13 at 12.32.37 AM.png)



2. 설치 후 도커를 열어서 실행.

![Screen Shot 2018-09-13 at 1.05.23 AM](/Users/seungyeonlee/Desktop/Screen Shot 2018-09-13 at 1.05.23 AM.png)



3. 터미널에 다음과 같이 입력

```
docker pull wnameless/oracle-xe-11g
```



4. 완료 후 다음과 같이 입력

```
docker run -d -p 59160:22 -p 59161:1521 wnameless/oracle-xe-11g
```



<br>

<br>

## Oracle Developer 설치

1. 아래 링크에서 Oracle developer를 다운로드 후 열기

http://www.oracle.com/technetwork/developer-tools/sql-developer/downloads/index.html



2. 왼쪽의 초록색 + 클릭

![Screen Shot 2018-09-13 at 1.28.00 AM](/Users/seungyeonlee/Desktop/Screen Shot 2018-09-13 at 1.28.00 AM.png)



3. 아래와 같이 입력 

   - **Connection Name:**  하고 싶은 이름 아무거나..

   - **Username:** system
   - **Password:** oracle
   - **Port:** 59161

   처음 유저를 만드는 것이기 때문에 꼭 위와 같게 해줘야한다.

![Screen Shot 2018-09-13 at 1.30.43 AM](/Users/seungyeonlee/Desktop/Screen Shot 2018-09-13 at 1.30.43 AM.png)



Test 버튼을 누르고 왼쪽 하단의 Status에 Success가 뜨는지 확인 후 Connect 버튼 클릭

![Screen Shot 2018-09-13 at 1.34.33 AM](/Users/seungyeonlee/Desktop/Screen Shot 2018-09-13 at 1.34.33 AM.png)



4. 성공!

Connections 아래에 test라는 데이터베이스가 생긴 것을 볼 수 있다.

![Screen Shot 2018-09-13 at 1.36.43 AM](/Users/seungyeonlee/Desktop/Screen Shot 2018-09-13 at 1.36.43 AM.png)

