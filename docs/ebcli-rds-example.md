# Amazon RDS DB 인스턴스를 Node.js 애플리케이션 환경에 추가


## package.json – MySQL을 이용한 Express
```
{
  "name": "my-app",
  "version": "0.0.1",
  "private": true,
  "dependencies": {
    "ejs": "latest",
    "aws-sdk": "latest",
    "express": "latest",
    "body-parser": "latest",
    "mysql": "latest"
  },
  "scripts": {
    "start": "node app.js"
  }
}
```

## Node.js용 드라이버 패키지
- MySQL – mysql
- PostgreSQL – pg
- Oracle – oracle
- SQL Server – mssql

## 데이터베이스에 연결
```
var mysql = require('mysql');

var connection = mysql.createConnection({
  host     : process.env.RDS_HOSTNAME,
  user     : process.env.RDS_USERNAME,
  password : process.env.RDS_PASSWORD,
  port     : process.env.RDS_PORT
});

connection.connect(function(err) {
  if (err) {
    console.error('Database connection failed: ' + err.stack);
    return;
  }

  console.log('Connected to database.');
});

connection.end();
```

## 환경변수 설정
```
1. Amazon RDS DB 인스턴스의 환경 속성을 구성하려면 Elastic Beanstalk 콘솔을 엽니다.
2. [Configuration]을 선택합니다.
3. [Software] 구성 카드에서 [Modify]를 선택합니다.

-   RDS_HOSTNAME – DB 인스턴스의 호스트 이름입니다.
-   RDS_PORT – DB 인스턴스가 연결을 허용하는 포트입니다. 기본값은 DB 엔진마다 다릅니다.
-   RDS_DB_NAME – 데이터베이스 이름(ebdb)입니다.
-   RDS_USERNAME – 데이터베이스에 대해 구성된 사용자 이름입니다.
-   RDS_PASSWORD – 데이터베이스에 대해 구성된 암호입니다.
```