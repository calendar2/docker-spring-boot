# Spring Boot 프로젝트를 Docker로 실행시키기

## 지식 정리

### 원리

1. Spring Boot 프로젝트를 빌드하면 build/libs 디렉토리에 ~~SNAPSHOT.jar 파일이 생성된다.
2. 프로젝트 내에 작성한 Dockerfile 명령어를 이용해 빌드 파일을 복사해서 실행시킨다.

### Dockerfile 명령어

```dockerfile
# 프로젝트를 동작시키는 자바 버전
# 나는 21버전으로 구축했기에 openjdk:21-jdk를 이용한다
FROM openjdk:21-jdk

# 빌드된 SNAPSHOT.jar 파일을 도커 컨테이너에 복사
# 이름은 app.jar로 변경해서 복사한다
COPY build/libs/*SNAPSHOT.jar app.jar

# 도커 컨테이너가 실행되면 root 디렉토리에 있는 app.jar 파일을 실행시킨다
ENTRYPOINT ["java", "-jar", "/app.jar"]
```

### docker cli
```bash
# Spring Boot 프로젝트 도커 이미지로 구축하기
docker build -t [이미지 이름] .

# 현재 가지고 있는 도커 이미지 리스트 조회
docker image ls

# 내가 만든 Spring Boot 도커 이미지를 도커 컨테이너로 실행시키기
# -d: 컨테이너를 백그라운드에서 실행하기
# -p: 호스트와 컨테이너의 포트 설정(BE 프로젝트니까 8080으로)
docker run -d -p 8080:8080 [이미지 이름]
```

### 강의 주소
[비전공자도 이해할 수 있는 Docker 입문/실전](https://inf.run/GvHgg)
