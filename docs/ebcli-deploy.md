# 환경 구성 및 배포


## eb create(환경구성)
```
$ eb create my-env
```

## eb status(상태확인)
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

## eb open(브라우저열기)
```
$ eb open eb-test-dev
```


## eb health 확인
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

