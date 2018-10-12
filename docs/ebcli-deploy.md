# 환경 구성 및 배포


### 환경생성
프로젝트 디렉토리 내에 소스코드가 있는 경우 이를 번들링하여 환경에 배포하고 그렇지 않으면 샘플 애플리케이션을 사용함.
```
$ eb create my-env
```

### 상태확인
```
$ eb status eb-test-dev

Environment details for: eb-test-dev
  Application name: eb-test
  Region: ap-northeast-2
  Deployed Version: Sample Application
  Environment ID: e-a3jqhpnkxr
  Platform: arn:aws:elasticbeanstalk:ap-northeast-2::platform/Node.js running on 64bit Amazon Linux/4.5.4
  Tier: WebServer-Standard-1.0
  CNAME: eb-test-endpoint.ap-northeast-2.elasticbeanstalk.com
  Updated: 2018-10-12 09:06:07.336000+00:00
  Status: Ready
  Health: Green
```

### 배포
```
$ eb deploy eb-test-dev
Creating application version archive "app-987b-181013_012600".
Uploading eb-test/app-987b-181013_012600.zip to S3. This may take a while.
Upload Complete.
2018-10-12 16:26:01    INFO    Environment update is starting.
2018-10-12 16:26:05    INFO    Deploying new version to instance(s).
2018-10-12 16:26:31    INFO    New application version was deployed to running EC2 instances.
2018-10-12 16:26:31    INFO    Environment update completed successfully.
```

### 브라우저열기
```
$ eb open eb-test-dev
```


### 헬스 체크
```
$ eb health eb-test-dev
 
eb-test-dev                                                                                                       Ok                                                                                                      2018-10-12 18:26:13WebServer                                                                                                                                                                                          Node.js running on 64bit Amazon Linux/4.5.4  total      ok    warning  degraded  severe    info   pending  unknown
  1        1        0        0        0        0        0        0

instance-id           status     cause                                                                                                                                                                                              health
  Overall             Ok
i-0b6c5f8bbbfdfcc1b   Ok

instance-id           r/sec    %2xx   %3xx   %4xx   %5xx      p99      p90      p75     p50     p10                                                                                                                               requests
  Overall             0.1     100.0    0.0    0.0    0.0    0.000*   0.000*   0.000   0.000   0.000
i-0b6c5f8bbbfdfcc1b   0.1         1      0      0      0    0.000*   0.000*   0.000   0.000   0.000

instance-id           type       az   running     load 1  load 5      user %  nice %  system %  idle %   iowait %                                                                                                                      cpu
i-0b6c5f8bbbfdfcc1b   t2.micro   2a   22 mins        0.0     0.0         0.3     0.0       0.1    99.5        0.1

instance-id           status     id   version              ago                                                                                                                                                                 deployments
i-0b6c5f8bbbfdfcc1b   Deployed   1    Sample Application   20 mins
```

