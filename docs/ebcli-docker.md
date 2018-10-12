# Docker & Elastic Beanstalk

### 단일 컨테이너 Docker
인스턴스 하나에 하나의 컨테이너 사용

### 멀티컨테이너 Docker
ECS를 사용하여 EB 환경에서 여러 컨테이너가 배포 됩니다.


### 사용 순서
```
git clone https://github.com/awslabs/eb-py-flask-signup.git
cd eb-py-flask-signup

// docker branch와 Docker profile연결
git checkout docker 
eb init -p Docker

// 환경 구성 
eb create dev-env
eb open
```

### 단일 컨테이너 구성
Dockerfile 사용자 이미지와 기존 이미지를 지정하는  Dockerrun.aws.json 파일 둘다가 포함되어 있어야 한다.

#### Dockerrun.aws.json
Docker 컨테이너를 Elastic Beanstalk 애플리케이션으로 배포하는 방법을 설명
- 이미지
```
기존 Docker 리포지토리에서 Docker 컨테이너를 구축할 Docker 기본 이미지를 지정합니다. 
Name 키의 값을 Docker 허브의 이미지의 경우에는 <organization>/<image name> 형식으로, 
다른 사이트의 경우에는 <site>/<organization name>/<image name> 형식으로 지정합니다.

Dockerrun.aws.json 파일에서 이미지를 지정하는 경우 
Elastic Beanstalk 환경의 각 인스턴스는 해당 이미지에서 docker pull을 실행합니다. 
경우에 따라 Update 키를 포함합니다. 기본값은 "true"로, Elastic Beanstalk에 리포지토리를 확인하고 
이미지에 대한 모든 업데이트를 가져와 캐시된 이미지를 덮어쓰도록 지시합니다.
```
- 포트
- 볼륨
- 로깅
- 인증
- 버전(AWSEBDockerrunVersion)(default 1)

#### Dockerrun.aws.json 예제
```
{
  "AWSEBDockerrunVersion": "1",
  "Image": {
    "Name": "janedoe/image",
    "Update": "true"
  },
  "Ports": [
    {
      "ContainerPort": "1234"
    }
  ],
  "Volumes": [
    {
      "HostDirectory": "/var/app/mydb",
      "ContainerDirectory": "/etc/mysql"
    }
  ],
  "Logging": "/var/log/nginx"
}
```

#### Dockerfile 예제
```
FROM ubuntu:12.04

RUN apt-get update
RUN apt-get install -y nginx zip curl

RUN echo "daemon off;" >> /etc/nginx/nginx.conf
RUN curl -o /usr/share/nginx/www/master.zip -L https://codeload.github.com/gabrielecirulli/2048/zip/master
RUN cd /usr/share/nginx/www/ && unzip master.zip && mv 2048-master/* . && rm -rf 2048-master master.zip

EXPOSE 80

CMD ["/usr/sbin/nginx", "-c", "/etc/nginx/nginx.conf"]
```



# Link
- [py flask signup github](https://github.com/aws-samples/eb-py-flask-signup/tree/docker)
- [단일 컨테이너 Docker 구성](https://docs.aws.amazon.com/ko_kr/elasticbeanstalk/latest/dg/create_deploy_docker_image.html)
