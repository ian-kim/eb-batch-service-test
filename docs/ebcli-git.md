# Elastic beanstalk & Git


### EB 초기화
아래와 같이 명령을 실행하면 EB CLI구성이 시작된다.
```
 $eb init
```

### 구성항목
- region 선택
- access key & secret key
- application 선택
- 플랫폼 및 언어
- SSH 연결 시 사용할 키
<br />

### 프로파일 사용
```
$ eb init --profile <profile-name>
```

### Git 브랜치와 Elastic Beanstalk 환경 연결
*Git 브랜치와 Elastic Beanstalk 환경 연결*을 하면 CD구성이 가능해진다.
```
$ git checkout master
$ eb use prod
$ git checkout develop
$ eb use dev
```

### 스테이지 명시하여 배포
```
$ eb deploy --staged
```

### 애플리케이션 버전에 Git 태그 할당
```
$ git tag -a v1.0 -m "My version 1.0"
```


# Link
[EB CLI와 GIT 사용](https://docs.aws.amazon.com/ko_kr/elasticbeanstalk/latest/dg/eb3-cli-git.html)
